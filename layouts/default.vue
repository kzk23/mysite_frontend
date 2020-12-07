<template>
    <b-navbar>
        <template slot="brand">
            <b-navbar-item tag="router-link" :to="{ path: '/' }">
                <img
                 src="https://raw.githubusercontent.com/buefy/buefy/dev/static/img/buefy-logo.png"
                  alt="Lightweight UI components for Vue.js based on Bulma"
                >
            </b-navbar-item>
        </template>
        <template slot="start">
            <b-navbar-item href="#">
                Home
            </b-navbar-item>
            <b-navbar-item href="#">
                Documentation
            </b-navbar-item>
            <b-navbar-dropdown label="Info">
                <b-navbar-item href="#">
                    About
                </b-navbar-item>
                <b-navbar-item href="#">
                    Contact
                </b-navbar-item>
            </b-navbar-dropdown>
        </template>

        <template slot="end">
            <b-navbar-item tag="div">
                <div class="buttons">
                    <a class="button is-primary">
                        <strong>Sign up</strong>
                    </a>
                    <a class="button is-light">
                        Log in
                    </a>
                </div>
            </b-navbar-item>
        </template>
    </b-navbar>

    <section class="main-content columns">
      <aside class="column is-2 section">
        <p class="menu-label is-hidden-touch">General</p>
        <ul class="menu-list">
          <li v-for="(item, key) of globalItems" :key="key">
            <nuxt-link :to="item.to" exact-active-class="is-active">
              <b-icon :icon="item.icon" />
              {{ item.title }}
            </nuxt-link>
          </li>
          <span v-if="loggedIn">
            <li v-for="(item, key) of authenticatedItems" :key="key">
              <nuxt-link :to="item.to" exact-active-class="is-active">
                <b-icon :icon="item.icon" />
                {{ item.title }}
              </nuxt-link>
            </li>
          </span>
        </ul>
      </aside>

      <div>
        <Nuxt />
      </div>
    </section>
</template>

<script>
import { mapState } from 'vuex'
export default {
  data() {
    return {
      globalItems: [
        {
          title: 'Home',
          icon: 'home',
          to: { name: 'index' },
        },
        {
          title: 'Blog',
          icon: 'book',
          to: { name: 'blog' },
        },
      ],
      authenticatedItems: [
        {
          title: 'Logout',
          icon: 'logout',
          to: { name: 'singed-out' },
        },
        {
          title: 'Post',
          icon: 'cogs',
          to: { name: 'post' },
        },
      ],
    }
  },
  computed: {
    ...mapState('auth', ['loggedIn']),
  },
}
</script>
<style>
html {
  font-family: 'Source Sans Pro', -apple-system, BlinkMacSystemFont, 'Segoe UI',
    Roboto, 'Helvetica Neue', Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
}
</style>
