<template>
  <v-container class="my-dashboard" fluid="fluid" fill-height="fill-height" text-xs-center="text-xs-center" v-bind:grid-list-sm="$vuetify.breakpoint.smAndDown" v-bind:grid-list-lg="$vuetify.breakpoint.mdAndUp">
    <v-layout row="row" wrap="wrap">
      <!-- Top Row-->
      <v-flex d-flex="d-flex" xs12="xs12" sm12="sm12" md6="md6">
        <v-card>
          <v-card-title>
            <div class="title">Sales</div>
          </v-card-title>
          <v-card-text style="position: relative; height: 100%; max-height: 400px;">
            <chart style="height: 100%;"></chart>
          </v-card-text>
        </v-card>
      </v-flex>
      <v-flex d-flex="d-flex" xs12="xs12" sm12="sm12" md6="md6">
        <v-card class="my-dashboard__pizza-status">
          <v-card-title>
            <div class="title">Status</div>
          </v-card-title>
          <v-card-text>
            <v-layout row="row" wrap="wrap">
              <v-flex xs4="xs4">
                <div class="sub-title">Order</div>
              </v-flex>
              <v-flex xs4="xs4">
                <div class="sub-title">Prep</div>
              </v-flex>
              <v-flex xs4="xs4">
                <div class="sub-title">Delivery</div>
              </v-flex>
              <v-flex d-flex="d-flex" xs4="xs4">
                <v-progress-circular class="my-dashboard__order" :size="100" :width="15" :rotate="360" :value="45" color="accent">45%</v-progress-circular>
              </v-flex>
              <v-flex d-flex="d-flex" xs4="xs4">
                <v-progress-circular :size="100" :width="15" :rotate="360" :value="75" color="primary">75%</v-progress-circular>
              </v-flex>
              <v-flex d-flex="d-flex" xs4="xs4">
                <v-progress-circular :size="100" :width="15" :rotate="360" :value="15" color="secondary">15%</v-progress-circular>
              </v-flex>
              <v-flex d-flex="d-flex" xs12="xs12">
                <line-chart style="height: 200px; width: 100%;"></line-chart>
              </v-flex>
            </v-layout>
          </v-card-text>
        </v-card>
      </v-flex>
      <!-- Bottom Row-->
      <v-flex d-flex="d-flex" xs12="xs12" sm12="sm12" md6="md6">
        <v-card>
          <v-card-title>
            <div class="title" style="margin-bottom: 47px;">Todo</div>
          </v-card-title>
          <v-date-picker v-model="date" min="2016-06-15" max="2018-03-20" full-width="full-width" :event-color="date =&gt; date[9] % 2 ? 'red' : 'yellow'" :events="functionEvents"></v-date-picker>
        </v-card>
      </v-flex>
      <v-flex d-flex="d-flex" xs12="xs12" sm12="sm12" md6="md6">
        <v-card>
          <v-card-media src="static/images/mountains.png" height="200px">
            <v-layout class="my-dashboard__media" column="column">
              <v-card-title class="white--text pl-5 pt-5">
                <div class="display-1 pl-5 pt-5">Main Contacts</div>
              </v-card-title>
            </v-layout>
          </v-card-media>
          <v-list two-line="two-line">
            <v-list-tile @click="">
              <v-list-tile-action>
                <v-icon>phone</v-icon>
              </v-list-tile-action>
              <v-list-tile-content>
                <v-list-tile-title>(650) 555-1234</v-list-tile-title>
                <v-list-tile-sub-title>Mobile</v-list-tile-sub-title>
              </v-list-tile-content>
            </v-list-tile>
          </v-list>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import store from './store' // eslint-disable-line no-unused-vars
import Chart from './components/chart'
import LineChart from './components/line-chart'

export default {
  name: 'Dashboard',

  components: {
    Chart,
    LineChart
  },

  data() {
    return {
      test: this.$store.state.dashboard.test,
      date: '2018-05-21'
    }
  },

  mounted() {},

  methods: {
    updateTest() {
      this.test++
        this.$store.dispatch('dashboard/updateTest', this.test)
    },
    functionEvents(date) {
      const [, , day] = date.split('-')
      return parseInt(day, 10) % 3 === 0
    }
  }
}
</script>

<style lang="stylus">
.my-dashboard

  &__media
    height: 100%
    margin: 0

  .picker__title
    display: none !important

</style>
