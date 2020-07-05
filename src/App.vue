<template>
  <div id="app">
    <div class="grid-buttons">
      <ButtonsObject v-on:click.native="numberOfPlayers = 2" nums="2" />
      <ButtonsObject v-on:click.native="numberOfPlayers = 3" nums="3" />
      <ButtonsObject v-on:click.native="numberOfPlayers = 4" nums="4" />
      <ButtonsObject v-on:click.native="numberOfPlayers = 5" nums="5" />

    </div>

    <div class="playGround">
      
      <FingerTouchObject v-if="this.numberOfPlayers>=2" color='#000000' playerNumber='1' class="one"/>
      <FingerTouchObject v-if="this.numberOfPlayers>=2" color='#24d957' playerNumber='2' class="two"/>
      <FingerTouchObject v-if="this.numberOfPlayers>=3" color='#9a138e' playerNumber='3' class="three"/>
      <FingerTouchObject v-if="this.numberOfPlayers>=4" color='#b07b01' playerNumber='4' class="four"/>
      <FingerTouchObject v-if="this.numberOfPlayers>=5" color='#2b5985' playerNumber='5' class="five"/>

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
      numberOfPlayers: 2
    };
  },
  components: {
    ButtonsObject,
    FingerTouchObject
  },
  methods:{
    
  }
}
</script>

<style>
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
}

.playGround .two{
  position: fixed;
  top:50%;
  right:10%;
}

.playGround .three{
  position: fixed;
  top:20%;
  left:20%;
}

.playGround .four{
  position: fixed;
  top:20%;
  right:20%;
}

.playGround .five{
  position: fixed;
  bottom:10%;
  left:40%;
}
</style>
