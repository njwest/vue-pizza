<template>
  <v-container
    class="my-tutorial"
    fluid="fluid"
    fill-height="fill-height"
    text-xs-center="text-xs-center"
  >
    <v-layout
      justify-center="justify-center"
      align-center="align-center"
    >
      <v-flex
        class="my-tutorial__hero"
        text-xs-center="text-xs-center"
      >
        <div>Check out the tutorial on the project's Github Wiki.<br><br></div>
        <div>
          <v-btn
            color="primay"
            href="https://github.com/prograhammer/vue-pizza/wiki"
            target="_blank">
            Go to Tutorial
          </v-btn>
        </div>
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
