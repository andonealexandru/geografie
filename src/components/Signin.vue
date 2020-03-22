<template>
  <div class="row">
    <div class="col s12">
      <form @submit.prevent="handleSubmit">
        <div class="row">
          <div class="uk-margin">
            <input v-model="formData.lastName" class="uk-input" type="text" placeholder="Nume" required>
          </div>
          <div class="uk-margin">
            <input v-model="formData.firstName" class="uk-input" type="text" placeholder="Prenume" required>
          </div>
        </div>
        <div class="row">
          <div class="uk-margin">
            <input v-model="formData.email" class="uk-input" type="email" placeholder="your@email.com" required>
          </div>
        </div>
        <div class="row">
          <div class="uk-margin">
            <input v-model="formData.password" class="uk-input" type="password" placeholder="Password" required>
          </div>
        </div>
        <div class="uk-margin">
          <select v-model="formData.classroom" class="uk-select" required>
            <option value="VlOGDlFT3HIUGNdq0V7t14zXf7PL0T">Clasa a V-a</option>
            <option value="lfJ2j7BDPt3f8VDd6qr31miSG4RCYh">Clasa a VI-a</option>
            <option value="bw7uA9bsk7TuNETjWnR3E2T4ZVA4x4">Clasa a VII-a</option>
            <option value="repRGY9WTfYC8X2l1plRHVfaKjEL6n">Clasa a VIII-a</option>
            <option value="vTjdSAoMx5hAycWSn1XmSq0ugXbByP">Clasa a IX-a A</option>
            <option value="LXpP5Qgyg73etwSA0DZbP78nVF8Hq2">Clasa a IX-a B</option>
            <option value="eHmvD7WqzS6ZNu92Y8OwmzNoaUpAi7">Clasa a IX-a C</option>
            <option value="czMNH5Nr2kBZe3cmNwVDZRY6fjuuxo">Clasa a IX-a D</option>
            <option value="7t59SlR3f9hOulb6VIwSNaW6314J8o">Clasa a IX-a E</option>
            <option value="BPcnnnYtThXlxmowdJrY4eFBQexcoR">Clasa a X-a A</option>
            <option value="Qv4CtBJCJCp5Gin5oxTj6fLoTiErDY">Clasa a X-a B</option>
            <option value="uzt2WWj4VKLpU5DI7T5f7VfpaH3ie7">Clasa a X-a C</option>
            <option value="UtPJoe9vKS27Y2ufdxeoHS7rTfTlTf">Clasa a X-a D</option>
            <option value="b2eSgf4cAZt2JWomJi3VeGFUHHFuAH">Clasa a X-a E</option>
            <option value="YECipiR2xknFUruLIqQ5e6uA1PVoBA">Clasa a XI-a A</option>
            <option value="wWWToX4YRc2YNTmg6mVwP3d3V9Za6s">Clasa a XI-a B</option>
            <option value="UrH8PghLbfRes6ds0iWlwSY4lPO7i5">Clasa a XI-a C</option>
            <option value="EKCJb5JBcoGXdx66SAU6XPn24BlUJ2">Clasa a XI-a D</option>
            <option value="idSy0wSEL5pQDDuZGIUL8DgAr3Abnk">Clasa a XI-a E</option>
            <option value="RPlSD8t1bLFqFH5BHuq1sXlfVSEeHo">Clasa a XII-a A</option>
            <option value="Q7KAhVyhXWBl84jBRyJSbEpBPy3B7O">Clasa a XII-a B</option>
            <option value="XI7dlEDkg1hRMfCV2aISUBAbZYQPzo">Clasa a XII-a C</option>
            <option value="gHZ6uw197sOWXx1O1B1cw0MCuPM5cz">Clasa a XII-a D</option>
            <option value="ze8QqrTO9Jwlov8048jKXYrfEYuFUu">Clasa a XII-a E</option>
          </select>
        </div>
        <div class="row">
          <div class="uk-margin">
            <input type="submit" :disabled="disabledButton" class="uk-button uk-button-default" value="Inregistrare">
            <p v-show="!showSpinner">{{ status }}</p>
            <div v-show="showSpinner">
              <vk-spinner class="uk-align-center" style="margin-top: 10px" />
            </div>
          </div>
        </div>

      </form>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
      name: "Signin",
      data () {
          return {
              formData: {
                  firstName: '',
                  lastName: '',
                  email: '',
                  password: '',
                  classroom: ''
              },
              responseData: {
                  userId: '',
                  classId: '',
                  firstName: '',
                  lastName: '',
                  email: ''
              },
              status: null,
              showSpinner: false,
              disabledButton: false
          }
      },
      methods: {
          handleSubmit: function () {
              let vm = this;
              this.showSpinner = true;
              this.disabledButton = true;
              let axiosConfig = {
                  headers: {
                      'Content-Type': 'application/json',
                      'Accept': 'application/json'
                  }
              };

              axios.post('https://geografie-backend.herokuapp.com/users', this.formData, axiosConfig)
                  .then(function (response) {
                      vm.responseData = response.data;
                      vm.showSpinner = false;
                      vm.status = "Verifica-ti adresa de mail pentru mail-ul de confirmare!"
                  })
                  .catch(function (error) {
                      vm.showSpinner = false;
                      vm.status = error.response.data.message;
                  })
          }
      }
  }
</script>

<style scoped>

</style>