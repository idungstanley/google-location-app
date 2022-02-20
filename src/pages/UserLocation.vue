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

<style>
.ui.button, .dot.circle.icon{
  background-color: #ff5a5f;
  color: white ;
}
</style>