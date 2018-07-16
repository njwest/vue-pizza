<template>
  <v-container class="my-login" fluid="fluid" fill-height="fill-height">
    <v-toolbar color="primary" flat="flat" dark="dark" fixed="fixed" app="app" dense="dense">
      <v-btn icon="icon"><img class="my-login__logo" src="~/@/assets/images/logo.svg" alt="VuePizza Logo" /></v-btn>
      <v-spacer></v-spacer>
      <v-btn flat="flat">GitHub</v-btn>
      <v-btn flat="flat">Tutorial</v-btn>
    </v-toolbar>
    <v-layout justify-center="justify-center" align-center="align-center">
      <v-flex class="text-xs-center" xs12="xs12" lg6="lg6">
        <v-layout row="row" wrap="wrap">
          <v-flex xs12="xs12">
            <div class="my-login__logo-name">
              <img src="~/@/assets/images/logo-name.svg" alt="VueExample" />
            </div>
          </v-flex>
          <v-flex xs12="xs12">
            <div class="my-login__subheading subheading">Examples by the Slice!</div>
          </v-flex>
          <v-flex xs12="xs12">
            <v-card class="my-login__card">
              <v-card-title class="my-login__card-title" primary-title="primary-title">
                <v-avatar :size="100">
                  <img src="~/@/assets/images/profile.jpg" alt="Avatar" />
                </v-avatar>
              </v-card-title>
              <v-card-text>
                <v-form>
                  <v-text-field label="E-mail" v-model="credentials.username" required="required"></v-text-field>
                  <v-text-field label="Password" hint="At least 8 characters" v-model="credentials.password" min="8" :append-icon="passwordHidden ? 'visibility' : 'visibility_off'" :append-icon-cb="() =&gt; (passwordHidden = !passwordHidden)"
                    :type="passwordHidden ? 'password' : 'text'" counter=""></v-text-field>
                </v-form>
              </v-card-text>
              <v-card-actions class="my-login__card-actions">
                  <v-btn :loading="loading" @click="login()" block="block" color="accent" dark="dark">Login</v-btn>
              </v-card-actions>
            </v-card>
          </v-flex>
        </v-layout>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import auth from '@/auth/helpers'

export default {
  name: 'LoginPage',

  data () {
    return {
      passwordHidden: true,
      credentials: {
        username: 'user@user.com',
        password: 'password'
      },
      error: '',
      loading: false
    }
  },

  methods: {
    login () {
      this.loading = true

      const credentials = {
        username: this.credentials.username,
        password: this.credentials.password
      }

      // auth.login(credentials, 'dashboard', ({isSuccess, data, errorMessage}) => {
      auth.fakeLogin(credentials, 'dashboard')
        .then((data) => {
          this.loading = false
        })
    }
  }
}
</script>

<style lang="stylus" scoped>
  .my-login
    background-color: $app-primary

    &__logo
      max-width: 46px
      padding-left: 12px
      padding-top: 4px

    &__logo-name

      img
        max-width: 200px
        width: 100%

    &__subheading
      color: white
      padding-top: 10px
      padding-bottom: 20px

    &__card
      max-width: 370px
      margin: 0 auto

    &__card-title
      justify-content: center

    &__card-actions
      justify-content: center

</style>
