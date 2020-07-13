<template>
  <v-app>
    <v-content>
      <HelloWorld/>
    </v-content>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';
var jssim = require('js-simulator');

export default {
  name: 'App',

  components: {
    HelloWorld,
  },

  data: () => ({
    //
  }),

  methods: () => ({
    data (){
      var sheduler = jssim.Scheduler();
      console.log(sheduler);
    }
  })
};
</script>
