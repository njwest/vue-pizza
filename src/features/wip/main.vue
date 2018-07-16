<template>
  <v-container
    class="my-wip"
    fluid="fluid"
    fill-height="fill-height"
    text-xs-center="text-xs-center"
  >
    <v-layout
      justify-center="justify-center"
      align-center="align-center"
    >
      <v-flex
        class="my-wip__hero"
        text-xs-center="text-xs-center">
        <img
          class="my-wip__cone"
          src="~/@/assets/images/traffic-cone.svg"
          alt="Work-in-progress"
        >
        <div>Work-in-progress</div>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  name: 'Wip',

  data () {
    return {
    }
  },

  mounted () {
  },

  methods: {

  }
}
</script>

<style lang="stylus" scoped>
.my-wip

  &__hero
    opacity 0.4

  &__cone
    width 100px

</style>
