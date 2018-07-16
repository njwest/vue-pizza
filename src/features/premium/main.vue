<template>
  <div
    class="my-prem-pts">
      <Appbar />
      <v-tabs
        class="elevation-0"
        dark="dark"
        v-model="currentTab"
        color="primary">
          <!-- @TODO: Paths don't matter here, only route names. Make issue to Vuetify.-->
          <v-tab
            v-bind:to="{ name: 'account', path: '/account' }"
            ripple="ripple">
            Profile
          </v-tab>
          <v-tab
            v-bind:to="{ name: 'billing', path: '/billing' }"
            ripple="ripple">
            Billing
          </v-tab>
          <v-tab
            v-bind:to="{ name: 'market-link', path: '/market-link' }"
            ripple="ripple">
            Market Link
          </v-tab>
          <v-tab
            v-bind:to="{ name: 'prem-pts', path: '/prem-pts' }"
            ripple="ripple">
            Premium Points
          </v-tab>
      </v-tabs>
      <div
        class="my-prem-pts__hero">
        <img
          class="my-prem-pts__cone"
          src="~/@/assets/images/traffic-cone.svg"
          alt="Under Construction" >
          <div>work-in-progress</div>
      </div>
  </div>
</template>

<script>
export default {
  name: 'PremPts',

  data () {
    return {
      currentTab: '/prem-pts'
    }
  },

  mounted () {
    // this.$store.dispatch('common/updateToolbar', {
    //  elevation: false
    // })
  },

  methods: {
  }
}
</script>

<style lang="stylus" scoped>
.my-prem-pts
  height 100%

  &__hero
    height 100%
    display flex
    justify-content center
    align-items center
    flex-direction column
    opacity 0.4

  &__cone
    width 100px
</style>
