<template>
  <!-- App -->
  <div id="app">
    <!-- Statusbar -->
    <f7-statusbar></f7-statusbar>
    <!-- Left Panel -->
    <f7-panel left reveal theme-dark>
      <f7-view url="/panel-left/"></f7-view>
    </f7-panel>

    <!-- Right Panel
    <f7-panel right cover theme-dark>
      <f7-view url="/panel-right/"></f7-view>
    </f7-panel> -->

    <!-- Main View -->
    <f7-view id="main-view" url="/" main></f7-view>

    <!-- Popup -->
    <f7-popup id="popup">
      <f7-view>
        <f7-page>
          <f7-navbar title="Popup">
            <f7-nav-right>
              <f7-link popup-close>Close</f7-link>
            </f7-nav-right>
          </f7-navbar>
          <f7-block>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Neque, architecto. Cupiditate laudantium rem nesciunt numquam, ipsam. Voluptates omnis, a inventore atque ratione aliquam. Omnis iusto nemo quos ullam obcaecati, quod.</f7-block>
        </f7-page>
      </f7-view>
    </f7-popup>

    <!-- Login Screen -->
    <f7-login-screen id="login-screen" v-bind:opened="loginScreenOpened">
      <f7-view>
        <f7-page login-screen>
          <f7-login-screen-title>Login</f7-login-screen-title>
          <f7-list form ref="form">
            <f7-list-item>
              <f7-label>Username</f7-label>
              <f7-input name="username" placeholder="Username" :value="teller" @input="teller = $event.target.value" type="text"></f7-input>
            </f7-list-item>
          </f7-list>
          <f7-list>
            <f7-list-button title="Sign In" v-on:click="loginUser(teller)"></f7-list-button>
            <f7-block-footer>
              <p>Click Sign In to close Login Screen</p>
              <p v-if="hasLoginError" class="red">{{ loginError }}</p>
            </f7-block-footer>
          </f7-list>
        </f7-page>
      </f7-view>
    </f7-login-screen>

  </div>
</template>

<script>
import axios from 'axios'
import { mapGetters, mapActions } from 'vuex'
export default {
  name: 'App',
  data: () => {
    return {
      errormsg: "",
      teller: null
    }
  },
  computed: {
    ...mapGetters([
      'isLoggedIn',
      'URL',
      'currentUser',
      'hasLoginError',
      'loginError'
    ]),
    loginScreenOpened: function() {
      return this.isLoggedIn == false
    },
    show_error: function() {
      return this.errormsg != "";
    }
  },
  created: function () {

  },
  methods: {
    ...mapActions([
      'loginUser',
      'getItems'
    ]),
  },
  watch: {
    isLoggedIn(isLoggedIn) {
      console.log("Now logged in")
      if(isLoggedIn) {
        this.getItems()
      }
    }
  }
}
</script>

<style>
  p.red {
    color: red;
  }
</style>
