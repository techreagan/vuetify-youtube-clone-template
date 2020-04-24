<template>
  <v-app>
    <!-- <NavBar v-if="!['SignIn', 'SignUp'].includes(this.$route.name)" /> -->
    <router-view name="NavBar"></router-view>
    <router-view name="StudioNavBar"></router-view>
    <v-content
      :class="{
        'content-bg': ![
          'SignIn',
          'SignUp',
          'Dashboard',
          'Video',
          'Detail'
        ].includes(this.$route.name)
          ? true
          : false
      }"
    >
      <router-view></router-view>
    </v-content>
  </v-app>
</template>

<script>
// import NavBar from '@/components/NavBar.vue'
export default {
  name: 'App',

  data: () => ({
    // hideNav: false
  })
  // components: {
  //   NavBar
  // }
}
</script>

<style lang="scss">
.content-bg {
  background-color: #f9f9f9;
}
.card {
  background: #f9f9f9 !important;
}
</style>
