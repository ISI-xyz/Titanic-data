<template>
  <v-card class="mx-auto" max-width="300" tile>
    <v-list shaped dense>
      <v-list-item-group v-model="item" color="primary">
        <v-btn @click="logout" class="mt-2" color="#0087ff" block text
          ><v-icon>mdi-logout</v-icon>Logout</v-btn
        >
      </v-list-item-group>
    </v-list>
  </v-card>
</template>
<script>
/* eslint-disable no-console */
export default {
  data: () => ({
    item: 1,
    items: [
      { text: 'Logout', icon: 'mdi-logout', link: '/login', action: 'logout' }
    ]
  }),
  computed: {
    authUser() {
      return this.$store.getters['users/loggedInUser']
    }
  },
  methods: {
    async login() {
      try {
        await this.$store.dispatch('auth/login', {
          email: this.email,
          password: this.password
        })
        this.email = null
        this.password = null
      } catch (e) {
        console.log(e)
      }
    },
    async goTo(val) {
      try {
        if (val === 'logout') {
          await this.$store.dispatch('users/logout')
        }
        console.log(`action of ${val} `)
      } catch (e) {
        this.formError = e.message
      }
    },
    async logout() {
      try {
        await this.$store.dispatch('users/logout')
      } catch (e) {
        this.formError = e.message
      }
    }
  }
}
</script>
