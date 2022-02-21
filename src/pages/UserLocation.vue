<template>
  <div>
    <section
      class="ui two column centered grid"
      style="position:relative; z-index:1;"
    >
      <div class="column">
        <form action="" class="ui segment large form">
          <div class="ui message red" v-show="error">{{ error }}</div>
          <div class="ui segment">
            <div class="field">
              <div
                class="ui right icon input large"
                :class="{ loading: spinner }"
              >
                <input
                  type="text"
                  placeholder="Enter your address  "
                  v-model="address"
                  id="autocomplete "
                />
                <i
                  class="dot circle link icon"
                  @click="locatorButtonPressed"
                ></i>
              </div>
            </div>
            <button class="ui button">Go</button>
          </div>
        </form>
      </div>
    </section>
    <section id="map"></section>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      address: "",
      error: "",
      spinner: false
    };
  },
  mounted() {
    new google.maps.places.Autocomplete(
      document.getElementById("autocomplete"),
      {
        bounds: new google.maps.LatLngBounds(
          new google.maps.LatLng(6.668867, 3.4516439)
        )
      }
    );
  },
  methods: {
    locatorButtonPressed() {
      this.spinner = true;

      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(
          position => {
            this.getAddressFrom(
              position.coords.latitude,
              position.coords.longitude
            );
          },
          error => {
            this.spinner = false;
            this.error =
              "The locator was denied permission to find you. Please type your address manually.";
            console.log(error.message);
          }
        );
      } else {
        this.spinner = false;
        this.error = error.message;
        console.log("Your Browswer does not support   geolocation api");
      }
    },
    getAddressFrom(lat, long) {
      axios
        .get(
          "https://maps.googleapis.com/maps/api/geocode/json?latlng=" +
            lat +
            "," +
            long +
            "&key=AIzaSyBDCcfybeHcMSBj7dhF2o3Oy2g2GtMa7w0"
        )
        .then(response => {
          if (response.data.error_message) {
            this.error = response.data.error_message;
            console.log(response.data.error_message);
          } else {
            this.address = response.data.results[0].formatted_address;
          }
          this.spinner = false;
        })
        .catch(error => {
          this.spinner = false;
          this.error = error.message;
          console.log(error.message);
        });
    }
  }
};
</script>
<style>
.ui.button,
.dot.circle.icon {
  background-color: #ff5a5f;
  color: white;
}
.pac-icon {
  display: none;
}
.pac-item {
  padding: 10px;
  font-size: 16px;
  cursor: pointer;
}
.pac-item:hover {
  background-color: #ececec;
}
.pac-item-query {
  font-size: 16px;
}
#map {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
}
</style>
