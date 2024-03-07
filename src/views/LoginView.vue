<script setup>
import { reactive, ref } from 'vue'
import router from '@/router'
import { useVuelidate } from '@vuelidate/core'
import { required, email as emailValidator, minLength } from '@vuelidate/validators'

const loginState = reactive({
  email: ref(''),
  password: ref('')
})
const showPassword = ref(false)
const rules = {
  email: { required, emailValidator },
  password: { required, minLength: minLength(6) }
}

const v$ = useVuelidate(rules, loginState)

function login() {
  if (v$.value.$invalid) return
  router.push('/game')
}
</script>

<template>
  <v-container class="mx-auto" >
    <v-card min-width="360" color="#181818">
      <v-card-title color="white">Login</v-card-title>
      <v-card-text>
        <v-form @submit.prevent="login">
          <v-text-field
            v-model="loginState.email"
            label="Email"
            :error-messages="v$.email.$errors"
          ></v-text-field>
          <v-text-field
            v-model="loginState.password"
            label="Password"
            :type="showPassword ? 'text' : 'password'"
            :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
            @click:append="showPassword = !showPassword"
            :error-messages="v$.password.$errors"
          ></v-text-field>
          <v-btn type="submit" color="green">Login</v-btn>
        </v-form>
      </v-card-text>
    </v-card>
  </v-container>
</template>
