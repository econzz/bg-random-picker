<template>
  <div id="app" >
    
    <div class="grid-buttons">
      <ButtonsObject v-on:click.native="numberOfPlayers = 2" nums="2" />
      <ButtonsObject v-on:click.native="numberOfPlayers = 3" nums="3" />
      <ButtonsObject v-on:click.native="numberOfPlayers = 4" nums="4" />
      <ButtonsObject v-on:click.native="numberOfPlayers = 5" nums="5" />

    </div>

    <div class="playGround">
      Player Confirmed: {{currentPressed}}
      
      <FingerTouchObject ref="touch1" @mouseup.native="onReleased" @mousedown.native="onClicked(1)" v-if="this.numberOfPlayers>=2" color='#000000' buttonId='1' class="one"/>
      <FingerTouchObject ref="touch2" @mouseup.native="onReleased" @mousedown.native="onClicked(2)" v-if="this.numberOfPlayers>=2" color='#24d957' buttonId='2' class="two"/>
      <FingerTouchObject ref="touch3" @mouseup.native="onReleased" @mousedown.native="onClicked(3)" v-if="this.numberOfPlayers>=3" color='#9a138e' buttonId='3' class="three"/>
      <FingerTouchObject ref="touch4" @mouseup.native="onReleased" @mousedown.native="onClicked(4)" v-if="this.numberOfPlayers>=4" color='#b07b01' buttonId='4' class="four"/>
      <FingerTouchObject ref="touch5" @mouseup.native="onReleased" @mousedown.native="onClicked(5)" v-if="this.numberOfPlayers>=5" color='#2b5985' buttonId='5' class="five"/>

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
      currentPressed:0
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
          self.$refs["touch"+buttonId].onClicked();
          self.onClicked(buttonId);
          break;

        case "6":
          buttonId = 1;
          if(!self.$refs["touch"+buttonId] ||self.$refs["touch"+buttonId].isClicked === false)
            return;
          self.$refs["touch"+buttonId].onReleased();
          self.onReleased(buttonId);
          break;
        case "7":
          buttonId = 2;
          if(!self.$refs["touch"+buttonId] ||self.$refs["touch"+buttonId].isClicked === false)
            return;
          self.$refs["touch"+buttonId].onReleased();
          self.onReleased(buttonId);
          break;
        case "8":
          buttonId = 3;
          if(!self.$refs["touch"+buttonId] ||self.$refs["touch"+buttonId].isClicked === false)
            return;
          self.$refs["touch"+buttonId].onReleased();
          self.onReleased(buttonId);
          break;
        case "9":
          buttonId = 4;
          if(!self.$refs["touch"+buttonId] ||self.$refs["touch"+buttonId].isClicked === false)
            return;
          self.$refs["touch"+buttonId].onReleased();
          self.onReleased(buttonId);
          break;
        case "0":
          buttonId = 5;
          if(!self.$refs["touch"+buttonId] ||self.$refs["touch"+buttonId].isClicked === false)
            return;
          self.$refs["touch"+buttonId].onReleased();
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

      for(let i = 1;i<=5;i++){
        if(this.$refs["touch"+i])
          this.$refs["touch"+i].reset();
      }

      
      
    },
    onClicked:function(number){// eslint-disable-line no-unused-vars
    
      console.log(this.$refs["touch"+number].isClicked);
      this.currentPressed+=1;
      if(this.currentPressed >= this.numberOfPlayers){
        this.currentPressed = this.numberOfPlayers;

      }
        this.startRandomize();


    },
    onReleased:function(event){// eslint-disable-line no-unused-vars
    

      this.currentPressed-=1;

      if(this.currentPressed <= 0)
        this.currentPressed = 0;

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

          var self = this;
        setTimeout(function(){
          self.reset();
        },2000);
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
