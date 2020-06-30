<template>
  <div class="buttons">
    
    <vs-button>{{num}}</vs-button>
    
  </div>
</template>

<script>
import { vsButton, vsSelect, vsPopup } from 'vuesax'
import 'vuesax/dist/vuesax.css'
import Vue from 'vue'
Vue.use(vsButton);
Vue.use(vsSelect);
Vue.use(vsPopup);

export default {
  name: 'ButtonsObject',
  props: {
    num:String
  },
  methods:{
      
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
