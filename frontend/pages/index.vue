<template>
  <section class="container">
    <div>
      <div v-if="loggedIn" class="content">
        <h2>ログイン中です</h2>
        <nuxt-link class="button is-warning" to="/logout">
          <span class="icon"><i class="fa fa-sign-out"></i></span>
          <span>Logout</span>
        </nuxt-link>
      </div>
      <div v-else class="content">
        <h2>ログインしてください</h2>
        <nuxt-link class="button is-primary" to="/login">
          <span class="icon"><i class="fa fa-sign-in"></i></span>
          <span>Login</span>
        </nuxt-link>
      </div>
      <button class="button is-primary"
        @click="ping"
      >
        Ping
      </button>
      <button class="button is-denger"
        @click="secured"
      >
        Secured
      </button>
    </div>
  </section>
</template>

<script>
export default {
  computed: {
    loggedIn() {
      return this.$auth0.isAuthenticated()
    }
  },
  methods: {
    async ping() {
      const ret = await this.$axios.$get('/api/v1/ping')
      console.log(ret);
    },
    async secured() {
      const ret = await this.$axios.$get('/api/v1/secured', {
        headers: {
          Authorization: "Bearer " + this.$auth0.getIdToken()
        }
      })
      console.log(ret)
    }
  }
}
</script>

<style>
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>

