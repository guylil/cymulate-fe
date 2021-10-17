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
        <v-col cols="4">

          <v-form
              ref="form"
              v-model="loginData.valid"
              lazy-validation
          >

            <v-text-field
                v-model="loginData.email"
                :rules="[v => !!v || 'Email is required']"
                label="E-mail"
                required
            ></v-text-field>

            <v-text-field
                v-model="loginData.name"
                :rules="[v => !!v || 'Password is required']"
                label="Password"
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
        name:'',
        email:'',
        valid: false
      },
    }),
    methods: {
      login(){
        this.loginData.valid = (this.loginData.name.length > 0 && this.loginData.email.length >0)
        if (this.loginData.valid){
          this.$router.push('/panel')
        } else {
          console.log('form is not valid')
        }

      },
      reset() {
        this.$router.push('/')
      }
    },

  }
</script>
