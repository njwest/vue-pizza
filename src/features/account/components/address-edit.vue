<template>
  <v-card class="my-profile-address" tile="tile">
    <v-toolbar card="card" dark="dark" color="primary">
      <v-btn icon="icon" @click.native="isActive = false" dark="dark">
        <v-icon>close</v-icon>
      </v-btn>
      <v-toolbar-title>Address</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-items>
        <v-btn dark="dark" flat="flat" @click.native="save()">Save</v-btn>
      </v-toolbar-items>
      <v-menu bottom="bottom" right="right" offset-y="offset-y">
        <v-btn slot="activator" dark="dark" icon="icon">
          <v-icon>more_vert</v-icon>
        </v-btn>
        <v-list></v-list>
      </v-menu>
    </v-toolbar>
    <v-card-text style="position: relative; max-width: 500px; margin: auto;">
      <loading :loading="loading" :oops="oops"></loading>
      <v-form v-model="valid">
        <!-- v-text-field(label="Name" v-model="name" :rules="nameRules" :counter="10" required="")-->
        <!-- v-text-field(label="E-mail" v-model="email" :rules="emailRules" required="")-->
        <v-text-field label="Address Line 1" v-model="address.addressLine1" :rules="rules.addressLine1" required=""></v-text-field>
        <v-text-field label="Address Line 2" v-model="address.addressLine2"></v-text-field>
        <v-text-field label="City" v-model="address.city"></v-text-field>
        <v-text-field label="State/Region" v-model="address.state" :rules="rules.state" required=""></v-text-field>
        <v-select label="Country" v-bind:items="countries" v-model="address.country" required="required" item-value="name" item-text="name" :rules="rules.country"></v-select>
        <v-text-field label="Zipcode" v-model="address.zipcode" :rules="rules.zipcode" required=""></v-text-field>
      </v-form>
    </v-card-text>
  </v-card>
</template>

<script>
import Service from '../service'
import countries from './countries'

export default {
  name: 'ProfileAddress',
  service: new Service(),

  props: {
    active: {
      type: Boolean,
      default: false
    }
  },

  data() {
    return {
      loading: false,
      showPage: false,
      oops: false,
      valid: false,

      /*
      name: '',
      nameRules: [
        (v) => !!v || 'Name is required',
        (v) => v.length <= 10 || 'Name must be less than 10 characters'
      ],
      email: '',
      emailRules: [
        (v) => !!v || 'E-mail is required',
        (v) => /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(v) || 'E-mail must be valid'
      ]
      */
      countries: countries,

      address: {
        addressLine1: '',
        addressLine2: '',
        city: '',
        state: '',
        country: null,
        zipcode: ''
      },

      rules: {
        addressLine1: [(v) => !!v || 'Address Line 1 is required'],
        state: [(v) => !!v || 'State/Region is required'],
        country: [(v) => !!v || 'Country is required'],
        zipcode: [(v) => !!v || 'Zipcode is required']
      }
    }
  },

  computed: {
    isActive: {
      get() {
        return this.active
      },
      set(val) {
        this.$emit('update:active', val)
      }
    }
  },

  watch: {
    active(val) {
      if (val) this.refreshData()
    }
  },

  mounted() {
    this.refreshData()
  },

  methods: {
    save() {
      this.isActive = false
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
          this.$store.dispatch('common/errorDialog', 'Error: ' + error.message)
          this.oops = true
          this.loading = false
        })
    }
  }
}
</script>

<style lang="stylus" scoped>
.my-profile-address
  height: 100%
</style>
