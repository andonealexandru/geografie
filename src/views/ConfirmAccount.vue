<template>
  <div>
    <div class="full-height uk-height-large uk-background-cover uk-light uk-flex" uk-parallax="bgy: -200" style="background-image: url('https://img5.goodfon.com/wallpaper/nbig/6/77/listia-rasteniia-fon.jpg');">
      <div class="uk-width-1-2@m uk-text-center uk-margin-auto uk-margin-auto-vertical">
        <div class="uk-padding">
          <h1 class="text" uk-parallax="opacity: 0,1; y: -100,0; scale: 2,1; viewport: 0.5;">{{status}}</h1>

          <vk-button type="text" @click="showLogin = true" class="buton uk-width-1-2@m uk-margin-auto">Conecteaza-te</vk-button>

        </div>
        <vk-modal :show.sync="showLogin" >
          <vk-modal-title>Log in</vk-modal-title>
          <Login />
        </vk-modal>
      </div>
    </div>
  </div>
</template>

<script>
    import Login from '../components/Login'
    import axios from "axios";
    export default {
        name: "ConfirmAccount",
        components: {
            Login
        },
        data () {
            return {
                showLogin: false,
                status: 'Validare cont...',
                response: ''
            }
        },
        created() {
            this.confirmAccount();
        },
        methods: {
            confirmAccount() {
                let vm = this;

                let axiosConfig = {
                    headers: {
                        'Content-Type': 'application/json',
                        'Accept': 'application/json'
                    }
                };

                axios.get('https://geografie-backend.herokuapp.com/users/confirm-account?token=' + this.$route.params.confirmationToken, axiosConfig)
                    .then(function (response) {
                        vm.response = response.data;
                        vm.status = "Acum te poti conecta la contul tau!";
                    })
                    .catch(function (error) {
                        vm.showSpinner = false;
                        vm.status = error.response.data.message;
                    })
            }
        }
    }
</script>

<style>
  .full-height {
    height: 100vh;
  }
  .text{
    font-size: 6vh;
    color: white;
    text-shadow: 2px 2px 4px #000000;
    font-family: Arial, Helvetica, sans-serif;
  }
  .buton{
    font-size: 3vh;
    text-shadow: 3px 3px 5px #000000;
    font-family: Arial, Helvetica, sans-serif;
  }
</style>