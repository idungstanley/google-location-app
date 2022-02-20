<template>
 <section class="ui two column centered grid">
   <div class="column">
     <form action="" class="ui segment large form">
       <div class="ui message red"></div>
       <div class="ui segment">
         <div class="field">
           <div class="ui right icon input large">
             <input type="text" placeholder="Enter your address">
             <i class="circle icon"></i>
           </div>
         </div>
         <button class="ui button" @click="locatorButtonPressed">Go</button>
       </div>
     </form>
   </div>
 </section>
</template>


<script>
export default {
  methods:{
    locatorButtonPressed(){
      if(navigator.geolocation){
navigator.geolocation.getCurrentPosition(position=>{
  console.log(position.coords.latitude);
  console.log(position.coords.longitude);
}),error=>{
  console.log(error.message);
}
      }else{
        console.log('Your Browswer does not support   geolocation api');
      }
    }
  }
}
</script>
<style>
.ui.button, .dot.circle.icon{
  background-color: #ff5a5f;
  color: white ;
}
</style>