<template>
  <v-container>
    <v-row class="text-center">

      <v-col class="mb-4">
        <h1 class="font-weight-bold mb-3">
          <div class=" mt-3">Welcome to Your Cool Cyber Tool</div>
        </h1>

        <p class=" font-weight-regular">
          Please login
        </p>
      </v-col>
    </v-row>


    <v-row class="justify-center">
        <v-col cols="6">

          <v-form
              ref="form"
              v-model="loginData.valid"
              lazy-validation
              @submit="login"
          >

            <v-text-field
                v-model="loginData.email"
                :rules="[v => !!v || 'Email is required']"
                label="E-mail"
                required
            ></v-text-field>

            <v-text-field
                v-model="loginData.password"
                :rules="[v => !!v || 'Password is required']"
                label="Password"
                type="password"
                required
            ></v-text-field>

              <v-btn
                  color="primary"
                  outlined
                  class="mr-4"
                  @click="login"
              >
                Login
              </v-btn>

              <v-btn

                  color="secondery"
                  outlined
                  class="mr-4"
                  @click="reset"
              >
                Forgot Password?
              </v-btn>

          </v-form>
        </v-col>
      </v-row>
    </v-container>
</template>

<script>
  export default {
    name: 'HelloWorld',

    data: () => ({
      loginData:{
        password:'',
        email:'',
        valid: false
      },
    }),
    methods: {
      login(){
        this.loginData.valid = (this.loginData.password.length > 0 && this.loginData.email.length >0)
        const init = {
          method: 'POST',
          headers: {Accept: 'application/json, text/plain, */*', 'Content-Type': 'application/json'},
          body: JSON.stringify({email: this.loginData.email, password:this.loginData.password}),
          mode: 'cors',
          cache: 'default'
        };
        fetch('http://localhost:3000/authenticate', init)
            .then(res => {
              if (res.status ===200){
                const data = res.json()
                data.then(response => {
                  if (response==='valid user'){
                    this.$router.push('/panel')
                  }
                }).catch(err => console.log('not valid: ',err))
              }
        }).catch(err => {
          console.log(err)
          this.loginData.password = ''
        })

      },
      reset() {
        this.$router.push('/')
      }
    },

  }
</script>
