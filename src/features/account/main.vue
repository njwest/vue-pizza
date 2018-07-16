<template>
  <v-container fluid="fluid" fill-height="fill-height" style="padding: 0;">
    <v-layout class="my-account" column="column">
      <v-tabs class="my-account__tabs" :color="$vuetify.breakpoint.smAndDown ? 'primary' : ''" :dark="$vuetify.breakpoint.smAndDown" v-model="currentTab" align-with-title="align-with-title" :class="{ 'my-account__mobile-tabs': $vuetify.breakpoint.mdAndUp }"
        style="position: fixed; width: 100%; z-index: 1; background: #F4F4F4;">
        <!-- @TODO: Paths don't matter here, only route names. Need to report this issue to Vuetify.-->
        <v-tab v-bind:to="{ name: 'account', path: '/account' }" ripple="ripple">Profile</v-tab>
        <v-tab v-bind:to="{ name: 'billing', path: '/billing' }" ripple="ripple">Billing</v-tab>
        <v-tab v-bind:to="{ name: 'premium', path: '/premium' }" ripple="ripple">Premium</v-tab>
      </v-tabs>
      <v-container fluid="fluid" fill-height="fill-height" v-bind:grid-list-sm="$vuetify.breakpoint.smAndDown" v-bind:grid-list-lg="$vuetify.breakpoint.mdAndUp" style="position: relative; margin-top: 40px;">
        <v-layout v-show="showPage" row="row" wrap="wrap">
          <v-flex d-flex="d-flex" xs12="xs12"></v-flex>
          <!-- Column left-->
          <v-flex d-flex="d-flex" xs12="xs12" md3="md3" lg4="lg4"></v-flex>
          <!-- Column right-->
          <v-flex d-flex="d-flex" xs12="xs12" md6="md6" lg4="lg4">
            <v-layout column="column">
              <v-flex d-flex="d-flex">
                <v-card>
                  <v-card-text>
                    <v-layout>
                      <v-flex>
                        <Gravatar :email="profile.email" :size="110"></Gravatar>
                        <!-- img.app-avatar(src="../../assets/images/profile.jpg")--><br/><a class="my-account__avatar-link" href="#">Update Avatar</a></v-flex>
                      <v-flex class="px-2">{{ profile.name }}
                        <v-btn flat="flat" icon="icon" color="primary">
                          <v-icon>edit</v-icon>
                        </v-btn><br/>Joined: January 2017<br/>Last login: 3:40PM EST 4/15/2017</v-flex>
                    </v-layout>
                  </v-card-text>
                </v-card>
              </v-flex>
              <v-flex d-flex="d-flex">
                <v-card flat="flat">
                  <v-card-title>
                    <div class="title">Credentials</div>
                  </v-card-title>
                  <v-card-text>
                    <v-layout row="row" wrap="wrap" style="align-items: center;">
                      <v-flex d-flex="d-flex" xs12="xs12" sm12="sm12" md6="md6">Email Address</v-flex>
                      <v-flex dflex="dflex" xs12="xs12" sm12="sm12" md6="md6">
                        <v-layout style="align-items: center;">
                          <v-flex class="text-xs-left" md6="md6">{{ profile.email }}</v-flex>
                          <v-flex class="text-xs-right" md6="md6">
                            <v-btn flat="flat" icon="icon" color="primary">
                              <v-icon>edit</v-icon>
                            </v-btn>
                          </v-flex>
                        </v-layout>
                      </v-flex>
                      <v-flex d-flex="d-flex" xs12="xs12" sm12="sm12" md6="md6">Password</v-flex>
                      <v-flex dflex="dflex" xs12="xs12" sm12="sm12" md6="md6">
                        <v-layout style="align-items: center;">
                          <v-flex class="text-xs-left" md6="md6">*********</v-flex>
                          <v-flex class="text-xs-right" md6="md6">
                            <v-btn flat="flat" icon="icon" color="primary">
                              <v-icon>edit</v-icon>
                            </v-btn>
                          </v-flex>
                        </v-layout>
                      </v-flex>
                    </v-layout>
                  </v-card-text>
                </v-card>
              </v-flex>
              <v-flex d-flex="d-flex">
                <v-card flat="flat">
                  <v-card-title>
                    <div class="title">Phone</div>
                  </v-card-title>
                  <v-card-text>
                    <v-layout style="align-items: center;">
                      <v-flex>+1 12343374839</v-flex>
                      <v-flex class="text-xs-right">
                        <v-btn flat="flat" icon="icon" color="primary">
                          <v-icon>edit</v-icon>
                        </v-btn>
                      </v-flex>
                    </v-layout>
                  </v-card-text>
                </v-card>
              </v-flex>
              <v-flex d-flex="d-flex">
                <v-card flat="flat">
                  <v-card-title>
                    <div class="title">Address</div>
                  </v-card-title>
                  <v-card-text>
                    <v-layout>
                      <v-flex>{{ profile.addressLine1 }}<template v-if="profile.addressLine2"><br/>{{ profile.addressLine2 }}</template><br/>{{ profile.city ? profile.city + ', ' : '' }} {{ profile.state }} {{ profile.zipcode }}<br/>{{ profile.country }}
                      </v-flex>
                      <v-flex class="text-xs-right">
                        <v-btn flat="flat" icon="icon" color="primary" @click="openDialogFull('AddressEdit')">
                          <v-icon>edit</v-icon>
                        </v-btn>
                      </v-flex>
                    </v-layout>
                  </v-card-text>
                </v-card>
              </v-flex>
              <v-flex d-flex="d-flex">
                <v-card flat="flat">
                  <v-card-title>
                    <div class="title">Account Options</div>
                  </v-card-title>
                  <v-card-text>
                    <v-layout></v-layout>
                  </v-card-text>
                </v-card>
              </v-flex>
            </v-layout>
          </v-flex>
        </v-layout>
      </v-container>
      <v-dialog v-model="dialogFullActive" fullscreen="fullscreen" transition="dialog-bottom-transition" scrollable="scrollable">
        <component :is="dialogFullComp" :active.sync="dialogFullActive"></component>
      </v-dialog>
    </v-layout>
  </v-container>
</template>

<script>
import AppFooter from '@/components/app-footer'
import AppBar from '@/components/app-bar'
import Service from './service'
import AddressEdit from './components/address-edit'
import Gravatar from 'vue-gravatar'

export default {
  name: 'Account',
  service: new Service(),

  components: {
    AppBar,
    AppFooter,
    Gravatar
  },

  data() {
    return {
      loading: false,
      showPage: false,
      oops: false,
      currentTab: '/account',
      dialogFullActive: false,
      dialogFullComp: null,
      profile: {
        email: '',
        name: '',
        country: '',
        addressLine1: '',
        addressLine2: '',
        state: '',
        zipcode: ''
      }
    }
  },

  mounted() {
    // this.$store.dispatch('common/updateToolbar', {
    //  elevation: false
    // })

    this.refreshData()
  },

  methods: {
    openDialogFull(comp) {
      if (comp === 'AddressEdit') this.dialogFullComp = AddressEdit

      this.dialogFullActive = true
    },

    refreshData() {
      this.loading = true
      this.oops = false

      this.$options.service.getProfile()
        .then((data) => {
          this.profile = data
          this.showPage = true
          this.loading = false
        })
        .catch((error) => {
          this.$store.dispatch('common/updateDialog', {
            show: true,
            text: 'Error: ' + error.message
          })
          this.oops = true
          this.loading = false
        })
    }
  }
}
</script>

<style lang="stylus">
  .my-account

    &__avatar-link
      padding-left: 10px

    &__oops
      width: 100px
      padding-bottom: 15px

    .tabs__bar
      background: #F4F4F4

    &__mobile-tabs
      .tabs__item--active
        color: $app-primary
</style>
