<template>
  <div id="app" v-bind:style="{background: colors, width: '100%', height: heights}">
    <div v-if="pathname === 'login'"></div>
    <div v-else>
      <b-navbar toggleable="lg" type="dark" variant="info">
        <b-navbar-brand href="/dashboard">MYC</b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <!-- <b-navbar-nav>
            <b-nav-item href="#">Link</b-nav-item>
            <b-nav-item href="#" disabled>Disabled</b-nav-item>
          </b-navbar-nav> -->

          <!-- Right aligned nav items -->
          <b-navbar-nav class="ml-auto">
            <!-- <b-nav-form>
              <b-form-input size="sm" class="mr-sm-2" placeholder="Search"></b-form-input>
              <b-button size="sm" class="my-2 my-sm-0" type="submit">Search</b-button>
            </b-nav-form> -->

            <!-- <b-nav-item-dropdown text="Lang" right>
              <b-dropdown-item href="#">EN</b-dropdown-item>
              <b-dropdown-item href="#">ES</b-dropdown-item>
              <b-dropdown-item href="#">RU</b-dropdown-item>
              <b-dropdown-item href="#">FA</b-dropdown-item>
            </b-nav-item-dropdown> -->

            <b-nav-item-dropdown right>
              <!-- Using 'button-content' slot -->
              <template v-slot:button-content>
                <em>User</em>
              </template>
              <!-- <b-dropdown-item href="#">Profile</b-dropdown-item> -->
              <b-dropdown-item href="#">
                <p>Profile</p>
                <b-list-group style="max-width: 300px;">
                  <b-list-group-item class="d-flex align-items-center">
                    <b-avatar class="mr-3"></b-avatar>
                    <span class="mr-auto">{{username}}</span>
                    <!-- <b-badge>5</b-badge> -->
                  </b-list-group-item>
                </b-list-group>
              </b-dropdown-item>
              <b-dropdown-item v-on:click="logOut">Sign Out</b-dropdown-item>
            </b-nav-item-dropdown>
          </b-navbar-nav>
        </b-collapse>
      </b-navbar>
    </div>
    <!-- <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div> -->
    <router-view/>
  </div>
</template>
<script>
export default {
  data () {
    return {
      colorlptt: '#29265b',
      colors: 'white',
      imagecolor: 'linear-gradient(to top, #051937, #0a4066, #006c96, #009cc3, #12cfeb)',
      // background-image: linear-gradient(to bottom, #051937, #0a4066, #006c96, #009cc3, #12cfeb);
      heights: '1000px',
      pathname: '',
      username: ''
    }
  },
  mounted () {
    if (window.location.pathname === '/') {
      this.pathname = 'login'
      console.log(this.pathname)
    }
    this.username = JSON.parse(localStorage.getItem('username'))
    console.log('username', this.username)
  },
  methods: {
    logOut () {
      console.log('logout')
      localStorage.removeItem('iat')
      localStorage.removeItem('username')
      localStorage.removeItem('jwt')
      localStorage.removeItem('role')
      location.replace('/')
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #29265b;;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
body, html {
  padding: 0;
  margin: 0;
  width: auto;
  height: 100%;
}
</style>
