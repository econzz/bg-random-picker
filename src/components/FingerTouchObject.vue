<template>
<div class="touchButton">
    <div class="playerNumber" v-if="this.playerNumber!=0" >{{playerNumber}}</div>
    <!-- <orbit-spinner v-if="this.isClicked===false"
  :animation-duration="1200"
  :size="100"
  color="#ff1d5e"
  @mousedown.native="onClicked"
/> -->

<spring-spinner v-if="this.isClicked===false && this.isMaster ===false"
  :animation-duration="3000"
  :size="100"
  :color="color"
  @mousedown.native="onClicked"
  @touchstart.native="onClicked"
  
/>
  
    <fulfilling-bouncing-circle-spinner v-if="this.isClicked===true && this.isMaster ===false"
  :animation-duration="4000"
  :size="100"
  color="#DAA520"
  @mouseup.native="onReleased"
  @touchend.native="onReleased"
/> 


<trinity-rings-spinner  v-if="this.isMaster ===true"
  :animation-duration="1500"
  :size="150"
  color="#ff1d5e"
/>
</div>
</template>

<script>
/*eslint no-unused-vars: "error"*/
import Vue from 'vue'
import { FulfillingBouncingCircleSpinner  } from 'epic-spinners'
import { TrinityRingsSpinner } from 'epic-spinners'
import { OrbitSpinner } from 'epic-spinners'// eslint-disable-line no-unused-vars
import { SpringSpinner } from 'epic-spinners'
Vue.use(OrbitSpinner );// eslint-disable-line no-unused-vars
Vue.use(FulfillingBouncingCircleSpinner );
Vue.use(SpringSpinner );
Vue.use(TrinityRingsSpinner );
export default {
  name: 'FingerTouchObject',
  data: function(){
    return{
      isClicked: false,
      isMaster:false,
      playerNumber:0,
    };
  },
  props: {
    
    color:String,
    buttonId:String
  },
  components: {
    // OrbitSpinner ,// eslint-disable-line no-unused-vars
    FulfillingBouncingCircleSpinner,
    SpringSpinner,
    TrinityRingsSpinner
  },
  methods:{
    
    onClicked:function(event){// eslint-disable-line no-unused-vars
        this.isClicked = true;
    },
    onReleased:function(event){// eslint-disable-line no-unused-vars
        this.isClicked = false;
    },
    setPlayerNumber:function(number){
      this.playerNumber = number;
      if(this.playerNumber === 1){
        this.markMaster();
      }
    },
    getPlayerNumber:function(){
      return this.playerNumber;
    },
    markMaster:function(){
      this.isMaster=true;
    },
    reset:function(){
      this.isMaster = false;
      this.isClicked = false;
      this.playerNumber = 0;
    },
  },
  created: function(){
    
  },
  mounted: function() {

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.touchButton{
    float:left;
}
.touchButton .playerNumber{
    
    
}
</style>
