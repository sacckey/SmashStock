<template>
  <div>
    <v-btn
      color="primary"
      @click="signIn"
    >Sign In</v-btn>
  </div>
</template>

<script>
export default {
  methods: {
    async signIn () {
      try {
        const provider = new this.$fireModule.auth.TwitterAuthProvider()
        const result = await this.$fire.auth.signInWithPopup(provider)
        console.log(result.user)
        // const token = await result.user.getIdToken()
        // this.$store.dispatch('setToken', token)
        this.$store.dispatch('setUser', result.user)

        this.$router.push('/')
      } catch (err) {
        this.showErrorAlert(err)
        this.$store.dispatch('resetState')
      }
    },
    async sampleLogin () {
      try {
        const authUser = await this.$axios.$post('v1/sessions/sample_login')
        this.$store.dispatch('setUser', authUser)
        this.$store.dispatch('setToken', authUser.auth_user.token)

        if (authUser.auth_user.is_first_login) {
          this.showAlert('Please update your AtCoder ID', 30, 'success')
          this.$router.push('/edit')
          return
        }

        this.$router.push('/')
      } catch (err) {
        this.showErrorAlert(err)
        this.$store.dispatch('resetState')
      }
    }
  }
}
</script>
