<template>
  <div class="card card-outline card-info">
    <div class="card-header text-center">
      <nuxt-link to="/" class="h3">Formulir Pendaftaran</nuxt-link>
    </div>
    <div class="card-body">
      <div v-if="validation.message" class="mt-2">
        <b-alert show variant="danger">{{ validation.message }}</b-alert>
      </div>
      <form @submit.prevent="login">
        <div class="form-group">
          <label>Email Address</label>
          <input type="text" v-model="user.email" :class="{ 'is-invalid': validation.email }" class="form-control"
            placeholder="Masukkan Email">
        </div>
        <div v-if="validation.email" class="mt-2">
          <b-alert show variant="danger">{{ validation.email[0] }}</b-alert>
        </div>

        <div class="form-group">
          <label>Password</label>
          <input type="password" v-model="user.password" :class="{ 'is-invalid': validation.password }"
            class="form-control" placeholder="Masukkan Password">
        </div>
        <div v-if="validation.password" class="mt-2">
          <b-alert show variant="danger">{{ validation.password[0] }}</b-alert>
        </div>

        <button type="submit" class="btn btn-info btn-block">Login</button>
      </form>
    </div>
    <!-- /.card-body -->
  </div>
</template>

<script>
export default {

  //layout
  layout: 'auth',

  //meta
  head() {
    return {
      title: 'Login | PRODI TI - Sistem Informasi Terpadu',
    }
  },

  data() {
    return {
      //state user
      user: {
        email: '',
        password: '',
      },
      //validation
      validation: []
    }
  },

  methods: {
    async login() {

      await this.$auth.loginWith('local', {
        data: {
          email: this.user.email,
          password: this.user.password
        }
      })

        .then(() => {

          //redirect
          this.$router.push({
            name: 'admin-pendaftaran'
          })

        })

        .catch(error => {
          //assign validation
          this.validation = error.response.data
        })
    }

  }

}
</script>

<style>
</style>
