<template>
  <div class="home">
    <div class="full-height uk-height-large uk-background-cover uk-light uk-flex" uk-parallax="bgy: -200" style="background-image: url('https://img5.goodfon.com/wallpaper/nbig/6/77/listia-rasteniia-fon.jpg');">
      <div class="uk-width-1-2@m uk-text-center uk-margin-auto uk-margin-auto-vertical">
        <h1 class="text" uk-parallax="opacity: 0,1; y: -100,0; scale: 2,1; viewport: 0.5;">Geografie</h1>

        <vk-button type="text" @click="showLogin = true" class="buton uk-width-1-2@m uk-margin-auto">Conecteaza-te</vk-button>
        <vk-button type="text" @click="showSignin = true" class="buton uk-width-1-2@m uk-margin-auto">Creeaza un cont</vk-button>

        <vk-modal :show.sync="showLogin" >
          <vk-modal-title>Log in</vk-modal-title>
          <Login />
        </vk-modal>

        <vk-modal :show.sync="showSignin" >
          <vk-modal-title>Sign in</vk-modal-title>
          <Signin />
        </vk-modal>

      </div>
    </div>
  </div>
</template>

<script>

    import Login from '../components/Login'
    import Signin from '../components/Signin'

    export default {
        name: 'Home',
        components: {
            Login,
            Signin
        },
        data() {
            return {
                showLogin: false,
                showSignin: false
            }
        }
    }
</script>

<style>
  .full-height {
    height: 100vh;
  }
  .text{
    font-size: 8vw;
    color: white;
    text-shadow: 2px 2px 4px #000000;
    font-family: Arial, Helvetica, sans-serif;
  }
  .buton{
    font-size: 20px;
    text-shadow: 3px 3px 5px #000000;
    font-family: Arial, Helvetica, sans-serif;
  }
</style>