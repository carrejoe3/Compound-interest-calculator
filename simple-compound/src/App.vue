<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center" id="titleBar">
        Compound Me
      </div>
    </v-app-bar>
    <v-content>
      <router-view></router-view>
    </v-content>
  </v-app>
</template>

<script>

import { Plugins } from '@capacitor/core'
const { SplashScreen } = Plugins

SplashScreen.hide()

export default {
  name: 'App'
}
</script>

<style lang="scss" scoped>
#titleBar {
  font-size: 1.5em;
  font-weight: 500;
}
</style>
