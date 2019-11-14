<template>
  <v-app>
    <v-content class="app">
      <v-container  fill-height>
        <transition name="fade" mode="out-in">
          <router-view />
        </transition>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
export default {
  name: 'App',
};
</script>

<style lang="scss">
html { overflow-y: auto !important }
::-webkit-scrollbar { 
    display: none; 
}

.fade-enter-active, .fade-leave-active {
  transition: opacity .3s ease;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
