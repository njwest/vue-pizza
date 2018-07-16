<template>
  <v-app>
    <transition
      name="slide"
      mode="out-in"
    >
      <router-view />
    </transition>
  </v-app>
</template>

<script>
export default {
  name: 'PublicLayout'
}
</script>

<style lang="stylus">

</style>
