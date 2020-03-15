<template>
  <div>
    <v-container class="fill-height" fluid>
      <v-row align="center" justify="center">
        <v-col cols="12" sm="8" md="4">
          <v-card class="elevation-12">
            <v-toolbar color="primary" dark flat>
              <v-toolbar-title>Iniciar sesión</v-toolbar-title>
            </v-toolbar>
            <v-card-text>
              <v-form @submit.prevent="handleLogin">
                <v-text-field
                  label="Usuario"
                  name="login"
                  prepend-icon="mdi-account-circle"
                  type="text"
                />
                <v-text-field
                  id="password"
                  label="Contraseña"
                  name="password"
                  prepend-icon="mdi-lock"
                  type="password"
                />
              </v-form>
            </v-card-text>
            <v-card-actions>
              <v-spacer />
              <v-btn color="primary" type="submit">Login</v-btn>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import User from '../models/user.model'

export default {
  name: 'Login',
  data() {
    return {
      user: new User('', ''),
      loading: false,
      message: ''
    }
  },
  computed: {
    loggedIn() {
      return this.$store.state.auth.status.loggedIn
    }
  },
  created() {
    if (this.loggedIn) {
      this.$router.push('/home')
    }
  },
  methods: {
    handleLogin() {
      this.loading = true
      this.$validator.validateAll().then(isValid => {
        if (!isValid) {
          this.loading = false
          return
        }

        if (this.user.username && this.user.password) {
          this.$store.dispatch('auth/login', this.user).then(
            () => {
              this.$router.push('/home')
            },
            error => {
              this.loading = false
              this.message =
                (error.response && error.response.data) ||
                error.message ||
                error.toString()
            }
          )
        }
      })
    }
  }
}
</script>

<style lang="scss" scoped></style>
