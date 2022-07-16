<template>
  <section class="container">
    <profile-card />
  </section>
</template>

<script>
import ProfileCard from '~/components/global/ProfileCard.vue'

export default {
  name: 'IndexPage',

  components: { 
    ProfileCard 
  },
}
</script>

<style lang="scss">
@import '~/assets/_color-palette.scss';

body {
  margin: 0 !important;
  padding: 0 !important;
  box-sizing: border-box !important;
}

.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 50vh;
  width: 100%;
  background-color: colorPaletteSetting(neutral-xtra-dark-blue);
}
</style>
