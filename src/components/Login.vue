<template>
  <div class="row">
    <div class="col s12">
      <form @submit.prevent="handleSubmit">
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
        <div class="row">
          <div class="uk-margin">
            <input type="submit" :disabled="disabledButton" class="uk-button uk-button-default" value="Conectare">
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
                        vm.status = error;
                    })
            }
        }
    }
</script>

<style scoped>

</style>