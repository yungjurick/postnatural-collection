<template>
  <div class="home" @click="navigateTo('collection')">
    <LogoComponent class="home__svg"/>
  </div>
</template>

<script>
import LogoComponent from '@/components/Logo.vue';
export default {
  name: 'home',
  components: {
    LogoComponent
  },
  methods: {
    navigateTo(dst) {
      this.$router.push('/collection');
    }
  }
};
</script>

<style lang="scss">
.home {
  position: fixed;
  display: flex;
  justify-content: center;
  align-items: center;
  top: 0;
  left: 0;
  height: 100vh;
  width: 100vw;
  cursor: zoom-in;
  &__svg {
    width: 50%;
  }
}
</style>
