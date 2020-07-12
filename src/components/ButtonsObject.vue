<template>
  
    
    <vs-button >{{nums}}</vs-button>
    

</template>

<script>
import { vsButton } from 'vuesax'
import 'vuesax/dist/vuesax.css'
import Vue from 'vue'
Vue.use(vsButton);

export default {
  name: 'ButtonsObject',
  props: {
    nums:String
  },
  methods:{
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


</style>
