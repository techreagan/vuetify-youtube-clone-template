<template>
  <v-container fluid class="fill-height">
    <v-row>
      <v-col cols="12" xs="12" sm="6" md="5" lg="4" class="ma-auto">
        <v-card class="px-8 pt-6 pb-12" outlined>
          <v-card-title class="text-center">VueTube</v-card-title>
          <v-card-subtitle class="mb-5">Sign in</v-card-subtitle>
          <v-card-text>
            <ValidationObserver ref="form" v-slot="{ handleSubmit, reset }">
              <form
                @submit.prevent="handleSubmit(signin)"
                @reset.prevent="reset"
              >
                <ValidationProvider
                  v-slot="{ errors }"
                  name="Email"
                  rules="required|email"
                >
                  <v-text-field
                    v-model="email"
                    :error-messages="errors"
                    label="Email"
                    outlined
                  ></v-text-field>
                </ValidationProvider>
                <ValidationProvider
                  v-slot="{ errors }"
                  name="Password"
                  rules="required"
                >
                  <p class="ma-0 text-right">
                    <v-btn
                      text
                      small
                      class="pl-0 text-capitalize"
                      color="primary"
                      href="true"
                      >Forget Password?</v-btn
                    >
                  </p>
                  <v-text-field
                    v-model="password"
                    type="password"
                    :error-messages="errors"
                    label="Password"
                    outlined
                  ></v-text-field>
                </ValidationProvider>
                <div class="mt-6 d-flex justify-space-between">
                  <v-btn
                    text
                    small
                    class="pl-0 text-capitalize"
                    color="primary"
                    router
                    to="signup"
                    >Create account</v-btn
                  >
                  <v-btn type="submit" class="primary" depressed>Sign in</v-btn>
                </div>
              </form>
            </ValidationObserver>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: 'SignIn',
  data: () => ({
    email: '',
    password: ''
  }),
  methods: {
    signin() {
      console.log('hello')
    }
  }
}
</script>

<style></style>
