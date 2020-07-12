<template>
  <div id="app" >
    
    <div class="grid-buttons">
      <ButtonsObject v-on:click.native="numberOfPlayers = 2" nums="2" />
      <ButtonsObject v-on:click.native="numberOfPlayers = 3" nums="3" />
      <ButtonsObject v-on:click.native="numberOfPlayers = 4" nums="4" />
      <ButtonsObject v-on:click.native="numberOfPlayers = 5" nums="5" />

    </div>

    <div class="playGround">
      <button class="reset" 
      @mousedown="reset()" 
      @touchstart="reset()">RESET</button>
      Player Confirmed: {{currentPressed}}
      <div v-if="this.currentPressed==this.numberOfPlayers">ALL PLAYER CONFIRMED! randoming in {{this.tick}}s</div>

      <FingerTouchObject ref="touch1" 
      @mouseup.native="onReleased(1)" 
      @touchend.native="onReleased(1)"
      @mousedown.native="onClicked(1)" 
      @touchstart.native="onClicked(1)"
      v-if="this.numberOfPlayers>=2" 
      color='#000000' 
      buttonId='1' 
      class="one"/>
      
      
      <FingerTouchObject ref="touch2" 
      @mouseup.native="onReleased(2)" 
      @touchend.native="onReleased(2)"
      @mousedown.native="onClicked(2)" 
      @touchstart.native="onClicked(2)"
      v-if="this.numberOfPlayers>=2" 
      color='#24d957' 
      buttonId='2' 
      class="two"/>

      <FingerTouchObject ref="touch3" 
      @mouseup.native="onReleased(3)" 
      @touchend.native="onReleased(3)"
      @mousedown.native="onClicked(3)" 
      @touchstart.native="onClicked(3)"
      v-if="this.numberOfPlayers>=3" 
      color='#9a138e' 
      buttonId='3' 
      class="three"/>

      <FingerTouchObject ref="touch4" 
      @mouseup.native="onReleased(4)" 
      @touchend.native="onReleased(4)"
      @mousedown.native="onClicked(4)" 
      @touchstart.native="onClicked(4)"
      v-if="this.numberOfPlayers>=4" 
      color='#b07b01' 
      buttonId='4' 
      class="four"/>

      <FingerTouchObject ref="touch5"
      @mouseup.native="onReleased(5)"
      @touchend.native="onReleased(5)"
      @mousedown.native="onClicked(5)" 
      @touchstart.native="onClicked(5)"
      v-if="this.numberOfPlayers>=5"
      color='#2b5985' buttonId='5' 
      class="five"/>

    </div>
  </div>
   
</template>

<script>
import ButtonsObject from './components/ButtonsObject.vue'
import FingerTouchObject from './components/FingerTouchObject.vue'

export default {
  name: 'App',
  data: function(){
    return{
      numberOfPlayers: 2,
      currentPressed:0,
      tick:3,
      interval: null,
      isDone:false,
    };
  },
  components: {
    ButtonsObject,
    FingerTouchObject
  },
  created(){
    
    
    
  },
  mounted() {
    this.reset();//reset before doing anything
    let self = this; 
    
    window.addEventListener('keyup', function(event) {
      event.preventDefault();
      if(!event.key)
        return;
      let buttonId = 1;

      switch(event.key){
        case "1":
        case "2":
        case "3":
        case "4":
        case "5":
          buttonId = event.key;
          if(!self.$refs["touch"+buttonId] || self.$refs["touch"+buttonId].isClicked)
            return;

          self.onClicked(buttonId);
          break;

        case "6":
          buttonId = 1;
          if(!self.$refs["touch"+buttonId] ||self.$refs["touch"+buttonId].isClicked === false)
            return;

          self.onReleased(buttonId);
          break;
        case "7":
          buttonId = 2;
          if(!self.$refs["touch"+buttonId] ||self.$refs["touch"+buttonId].isClicked === false)
            return;

          self.onReleased(buttonId);
          break;
        case "8":
          buttonId = 3;
          if(!self.$refs["touch"+buttonId] ||self.$refs["touch"+buttonId].isClicked === false)
            return;

          self.onReleased(buttonId);
          break;
        case "9":
          buttonId = 4;
          if(!self.$refs["touch"+buttonId] ||self.$refs["touch"+buttonId].isClicked === false)
            return;

          self.onReleased(buttonId);
          break;
        case "0":
          buttonId = 5;
          if(!self.$refs["touch"+buttonId] ||self.$refs["touch"+buttonId].isClicked === false)
            return;

          self.onReleased(buttonId);
          break;
      }
        
        //self.myMethod(ev); // declared in your component methods
    });

    
  },
  methods:{
    reset:function(){

      this.numberOfPlayers=2;
      this.currentPressed=0;
      this.tick = 3;
      this.isDone = false;
      for(let i = 1;i<=5;i++){
        if(this.$refs["touch"+i])
          this.$refs["touch"+i].reset();
      }

      
      
    },
    onClicked:function(number){// eslint-disable-line no-unused-vars

      if(this.isDone)
        return;

      if(!this.$refs["touch"+number] || this.$refs["touch"+number].isClicked)
        return;
        
      this.$refs["touch"+number].onClicked();

      this.currentPressed+=1;
      if(this.currentPressed >= this.numberOfPlayers){
        this.currentPressed = this.numberOfPlayers;

      }
        this.checkForRandomize();


    },
    onReleased:function(number){// eslint-disable-line no-unused-vars

      if(this.isDone)
        return;

      if(!this.$refs["touch"+number] || this.$refs["touch"+number].isClicked === false)
        return;
        

      this.$refs["touch"+number].onReleased();

      this.currentPressed-=1;
      
      if(this.currentPressed <= 0)
        this.currentPressed = 0;

      this.checkForRandomize();
    },
    checkForRandomize:function(){
      if(this.currentPressed === this.numberOfPlayers){
        this.interval = setInterval(this.incrementTime, 1000);
      }
      else{
        this.tick = 3;
        clearInterval(this.interval);
        console.log('timer stops');
      }
    },
    incrementTime() {
      this.tick -=1; 
      if(this.tick <= 0){
        this.tick = 0;
        clearInterval(this.interval);
        console.log('start randoming!');
        this.startRandomize();
      }
    },
    startRandomize:function(){
      let result=[];
      if(this.currentPressed === this.numberOfPlayers){
          for(let i =1;i<=this.numberOfPlayers;i++){
            result.push(i);
          }

          let randomizedResult = this.shuffleArray(result);

          for(let j=0;j<randomizedResult.length;j++){
             this.$refs["touch"+(j+1)].setPlayerNumber(randomizedResult[j]);
          }

        this.isDone = true;
      }
    },
    shuffleArray:function(array) {
      /* Randomize array in-place using Durstenfeld shuffle algorithm */
       for (var i = array.length - 1; i > 0; i--) {
          var j = Math.floor(Math.random() * (i + 1));
          var temp = array[i];
          array[i] = array[j];
          array[j] = temp;
      }
      return array;
    }
  }
}
</script>

<style>
* {
  -webkit-touch-callout: none;
  
  /* iOS Safari */
  -webkit-user-select: none;
  
  /* Safari */
  -khtml-user-select: none;
  
  /* Konqueror HTML */
  -moz-user-select: none;
  
  /* Firefox */
  -ms-user-select: none;
  
  /* Internet Explorer/Edge */
  user-select: none;
  
  /* Non-prefixed version, currently supported by Chrome and Opera */
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.grid-buttons {
  display: grid;
  grid-template-columns: auto auto auto auto;
  grid-gap: 10px;
  padding: 10px;
  
}

.grid-buttons button {
 
  text-align: center;
  font-size: 30px;
}

.playGround{
  background-color: antiquewhite;
  position: fixed;
  width:100%;
  height:100%;
}

.playGround .one{
  position: fixed;
  top:50%;
  left:10%;
  color:'#000000';
}

.playGround .two{
  position: fixed;
  top:50%;
  right:10%;
  color:'#24d957';
}

.playGround .three{
  position: fixed;
  top:20%;
  left:20%;
  color:'#9a138e';
}

.playGround .four{
  position: fixed;
  top:20%;
  right:20%;
  color:'#b07b01';
}

.playGround .five{
  position: fixed;
  bottom:10%;
  left:40%;
  color:'#2b5985';
}
</style>
