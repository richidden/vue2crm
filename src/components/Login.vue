<template>
<v-container fill-height justify-center align-center >
  <!-- <v-layout row > -->
    <v-flex xs12 sm8 md4>
      <!-- <h1> &nbsp;</h1> -->
      <v-card class="elevation-12">
          <v-card-title class="blue darken-1">
            <h4 style="color:white">Vue-CRM</h4>
          </v-card-title>
          <v-card-text>
              <form @submit.prevent="login">
                <v-layout row>
                  <v-flex hidden-xs-only sm4>
                    <v-subheader>User ID</v-subheader>
                  </v-flex>
                  <v-flex xs12 sm8>
                    <v-text-field class="input-group--focused" name="email" v-model="email" label="email" value="Input text"></v-text-field>
                  </v-flex>
                </v-layout>
                <v-layout row>
                  <v-flex hidden-xs-only sm4>
                    <v-subheader>Password</v-subheader>
                  </v-flex>
                  <v-flex xs12 sm8>
                    <v-text-field class="input-group--focused" name="password" type="password" v-model="pass" label="password" value="Input text"></v-text-field>
                  </v-flex>
                </v-layout>
                <v-btn type="submit">login</v-btn>
                <v-snackbar v-if="error" :timeout="timeout" :top="true" :multi-line="mode === 'multi-line'" :vertical="mode === 'vertical'" v-model="error">
                  {{ text }}
                  <v-btn class="pink--text" flat @click.native="error = false">Close</v-btn>
                </v-snackbar>
              </form>
        </v-card-text>
      </v-card>
    </v-flex>
  <!-- </v-layout> -->
  </v-container>
</template>
<script>
import auth from '../utils/auth'

export default {
  data () {
    return {
      email: 'admin@test.com',
      pass: 'password',
      error: false,
      text: ''
    }
  },
  methods: {
    login () {
      auth.login(this.email, this.pass, (loggedIn, err) => {
        if (err) {
          console.log('login', err)
          this.error = true
          this.text = err
        } else if (loggedIn === false) {
          console.log('login', loggedIn)
          this.error = true
          this.text = 'Bad login information'
        } else {
          console.log(this.$route)
          this.$router.push(this.$route.query.redirect || '/')
        }
      })
    }
  }
}
</script>
<style lang="stylus">
  @import '../stylus/main'
</style>
