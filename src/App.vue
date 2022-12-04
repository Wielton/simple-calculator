<template>
  <v-app app>
    <v-main app>
      <HelloWorld/>
    </v-main>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';

export default {
  name: 'App',

  components: {
    HelloWorld,
  },

  data: () => ({
    //
  }),
};
</script>
<style lang="scss" scoped>
* {
  background-color: #383838;
  
}
</style>