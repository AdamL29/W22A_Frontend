<template>
  <v-app>
    <v-main>
      <router-view/>
    </v-main>
  </v-app>
</template>

<script>
import {RouterView} from 'vue-router';

export default {
  name: 'App',
  components: {
    RouterView
  },
};
</script>

<style scoped>
*{
  margin: 0;
  padding: 0;
}
</style>