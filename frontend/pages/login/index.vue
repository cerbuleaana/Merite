<template>
  <div>
       <Sidebar>
     <ul class="sidebar-panel-nav">
       <li><nuxt-link class="item" to="/">à propos</nuxt-link></li>
       <li><nuxt-link class="item" to="/">besoin d'aide ?</nuxt-link></li>
     </ul>
   </Sidebar>

    <div class="login-background">
      <div class="left"></div>
      <div class="right"></div>
    </div>
    <div class="login-container">
      <div class="nav-login">
        <div class="login-title">
          <h1>Merite</h1>
        </div>
        <div v-if="window.width > 660" class="items">
          <nuxt-link class="item" to="/">à propos</nuxt-link>
          <nuxt-link class="item" to="/">besoin d'aide ?</nuxt-link>
        </div>
        <Burger v-else></Burger>

      </div>

      <div class="login-body">
        <div class="login-form-container">
          <form ref="connect_form" @submit.prevent="connect" class="login-form">
            <h2>Content de vous revoir</h2>
            <input type="text" v-model="form.username" class="login-form-input" placeholder="Nom d'utilisateur">
            <input type="password" v-model="form.password" class="login-form-input" placeholder="Mot de passe">
            <div class="mdpoublie">
              <div class="stay-connect">
                <input type="checkbox" name="stay-connect" id=""><label for="stay-connect">Rester connecté ?</label>
              </div>
              <nuxt-link to="/">mot de passe oublié ?</nuxt-link>
            </div>
            <button id="login-connexion">Connexion</button>
          </form>
        </div>
        <div class="login-content">
          <img id="login-content-illustration" src="~/assets/login/login-illustration.png" alt="illustration">
        </div>
      </div>
      <div class="login-footer">
        <p class="login-copyright">© Copyright Merite.com</p>
      </div>
    </div>

  </div>
</template>

<script>
import Burger from '~/components/Burger.vue';
import Sidebar from '~/components/Sidebar.vue';

  export default {
    components : { Burger, Sidebar },
    data() {
      return {
        window: {
          height: 0,
          width: 0
        },
        form : {
          username : '',
          password : ''
        },
        hambOpen: false
      }
    },
    created() {
      if (process.client) {
        window.addEventListener("resize", this.winResize);
        this.window.width = window.innerWidth
      }
    },
    destroyed() {
      if (process.client) {
        window.removeEventListener("resize", this.winResize);

      }
    },
    methods: {
      async connect() {
        console.log(this.form.username);
        console.log({username : this.form.username, password : this.form.password});
      },
      winResize(e) {
        if (process.client) {

          this.window.width = window.innerWidth
        }
      },
      toggleHamb() {
        this.hambOpen = !this.hambOpen
        console.log(this.hambOpen);
      }
    }
  }

</script>

<style lang="scss">
 ul.sidebar-panel-nav {
   list-style-type: none;
 }

 ul.sidebar-panel-nav > li > a {
   color: #fff;
   text-decoration: none;
   font-size: 1.5rem;
   display: block;
   padding-bottom: 0.5em;
 }

  .login-background {
    position: absolute;
    height: 100vh;
    width: 100vw;
    z-index: -1;
    display: flex;
    flex-direction: row;
    justify-content: space-between;

    .left {
      background-color: #fff;
      width: 50vw;
      height: 100vh;
    }

    .right {
      background-color: #00A8FF;
      opacity: 0.19;
      width: 50vw;
      height: 100vh;
    }
  }

  .login-container {
    height: 100vh;
    width: 100vw;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }

  @media screen and (max-width : 660px) {
    .nav-login {
      padding: 0 20px !important;
    }

    .mdpoublie {
      flex-direction: column;

      .stay-connect {
        margin: 0 10px;
      }
    }
  }

  .nav-login {
    font-family: 'Poppins';
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    height: 80px;
    padding: 0 100px;
    transition: .3s;



    .login-title {
      font-family: 'Montserrat';
      text-transform: uppercase;
      font-weight: bold;
    }

    .items {
      font-weight: 600;
    }
  }

  .item {
    margin: 0 20px;
    text-decoration: none;
    color: #000;
    transition: .3s;

    &:hover {
      color: #00A8FF;
    }
  }

  .hamburger-menu {
    cursor: pointer;
  }

  .middle.close {
    &::after {
      display: block;
      transform: rotateZ(45deg);
      width: 40px;
      opacity: 1;
    }

    &::before {
      display: block;
      transform: rotateZ(-45deg);
      width: 40px;
      opacity: 1;
    }

    height: 0;
    width: 0;
  }


  .dropdown-hamb {
    position: absolute;
    top: 0;
    background: #f9f7ff;
    width: 100vw;
    height: 100px;
    left: 0;
    top: 80px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

    .item {
      text-decoration: none;
      margin: 5px;
    }
  }

  .middle {
    height: 4px;
    width: 30px;
    background-color: #000;
    position: relative;
    display: block;
    transition: .2s;

    &::after {
      content: '';
      position: absolute;
      height: 4px;
      width: 20px;
      right: 0;
      background-color: #000;
      transform: translateY(10px);
    }

    &::before {
      content: '';
      position: absolute;
      height: 4px;
      width: 40px;
      right: 0;
      background-color: #000;
      transform: translateY(-10px);
    }
  }

  .login-body {
    display: flex;
    flex-direction: row;
    justify-content: space-around;

    .login-form-container {
      display: flex;
      justify-content: center;
      align-items: center;
      width: 50%;
    }

  }

  .login-form {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

    h2 {
      padding-bottom: 50px;
    }


    .login-form-input {
      border: none;
      font-family: 'Poppins';
      font-weight: 600;
      height: 30px;
      width: 100%;
      background: #FFFFFF;
      box-shadow: 0px 4px 7px -1px rgba(0, 0, 0, 0.25);
      border-radius: 4px;
      margin: 20px 10px;
      padding: 25px 20px;

      &:focus,
      &:active {
        border: none;
        outline: none;
      }
    }
  }

  #login-content-illustration {
    transform: translateX(-100px);
    transition: .3s;
  }

  .login-content {
    transition: .3s;
  }

  @media screen and (max-width : 1400px) {
    #login-content-illustration {
      display: none;
    }

    .right {
      display: none;
    }

    .login-body {
      justify-content: center;
    }
  }

  @media screen and (max-width : 620px) {

    .login-body .login-form-container {
      width: 65%;
    }
  }

  .mdpoublie {
    display: flex;
    justify-content: space-between;
    width: 100%;
    align-items: center;
    height: 20px;
    font-size: .7em;

    .stay-connect {
      display: flex;
      flex-direction: row;
      align-items: center;
      justify-content: flex-start;

      label {
        padding-left: 10px;
      }
    }
  }

  #login-connexion {
    color: #fff;
    width: 100%;
    border: none;
    background: #130f40;
    box-shadow: 0px 4px 7px -1px rgba(0, 0, 0, 0.25);
    border-radius: 4px;
    font-weight: 600;
    font-size: 1.3em;
    margin-top: 40px;
    height: 56px;
    cursor: pointer;
    transition: .3s;

    &:hover {
      transform: scale(.97);
      background: #130f40de;

    }
  }

  .login-footer {
    height: 50px;
    margin-top: 50px;
  }

  .login-copyright {
    text-align: center;
    font-weight: 600;
  }

  .slide-fade-enter-active {
    transition: all .3s ease;
  }

  .slide-fade-leave-active {
    transition: all .3s ease;
  }

  .slide-fade-enter,
  .slide-fade-leave-to {
    transform: translateY(-10px);
    opacity: 0;
  }

</style>
