<template>
  <div class="container-fluid">
    <b-card class="mb-5">
      <div>
        <b-form @submit.stop.prevent>
          <label for="searchPartners">Find a user</label>
          <b-row>
            <b-input id="searchPartners" v-model="idUser" class="col-9 mr-3" type="text" aria-describedby="password-help-block" />
            <b-button type="button" class="btn-primary col-1" @click="fetchSomething">
              Recherhcer
            </b-button>
          </b-row>
          <b-form-text id="password-help-block" class="">
            Please type into the form the phone number of the user, that you want to add like partners
          </b-form-text>
        </b-form>
      </div>
    </b-card>
    <div class="container">
      <facebook-loader
        v-if="isLoading"
        :speed="2"
        class="mb-5"
      />
      <div v-if="userPartners ==null" class="card mb-5" style="max-width: 100%;">
        <p> Please find a user in form</p>
      </div>
      <div v-if="userPartners" class="card mb-5" style="max-width: 100%;">
        <div class="row no-gutters">
          <div class="col-md-5" style="background: #868e96;">
            <img src="https://mdbootstrap.com/img/Photos/Avatars/img%20(20).jpg" class="card-img-top h-100" alt="...">
          </div>
          <div class="col-md-7">
            <div class="card-body">
              <h5 class="card-title">
                {{ userPartners.name }}
              </h5>
              <ul>
                <li>Prenom: {{ userPartners.surname }}</li>
                <li>Telephone: {{ userPartners.phoneNumber }}</li>
                <li>UIID: {{ userPartners.uid }}</li>
              </ul>
              <b-button class="btn btn-success " @click="createPartners">
                View Profile
              </b-button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { FacebookLoader } from 'vue-content-loader'

export default {
  name: 'AddPartners',
  components: {
    FacebookLoader
  },
  data () {
    return {
      isLoading: false,
      idUser: null,
      userPartners: null,
      notFound: false,
      responseError: false
    }
  },
  methods: {
    async fetchSomething (e) {
      e.preventDefault()
      this.isLoading = true

      try {
        const result = await this.$axios.$get(`http://52.29.136.52/api/users/${this.idUser}`)
        this.userPartners = result

        this.isLoading = false
      } catch (error) {
        const responseStatus = error.response.status
        console.log(Object.keys(error), error.response.status)
        if (responseStatus === 404) {
          this.notFound = true
          console.log('User not found')
        } else {
          this.responseError = true
        }
        this.isLoading = false
      }
    },
    async createPartners () {
      console.log(this.userPartners.phoneNumber)
      try {
        const result = await this.$axios.$post('http://reservation.cooltrip.it/api/user/partner',
          {
            lastname: this.userPartners.name,
            firstname: this.userPartners.surname,
            phoneNumber: this.userPartners.phoneNumber,
            uiid: this.userPartners.uid
          },
          {
            headers: {
              'Access-Control-Allow-Origin': '*',
              'Content-Type': 'application/json',
              'Access-Control-Allow-Methods': 'GET, PUT, POST, DELETE, OPTIONS'
            }

          }

        )
        console.log(result, 'Partners created')
      } catch (error) {
        console.log(Object.keys(error))
      }
    }
  }
}
</script>

<style scoped>

</style>
