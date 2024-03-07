<script setup>
import { reactive, ref } from 'vue'
import router from '@/router'
import { useVuelidate } from '@vuelidate/core'
import { required, email as emailValidator, minLength } from '@vuelidate/validators'

const loginState = reactive({
  email: '',
  password: ''
})
const rules = {
  email: { required, emailValidator },
  password: { required, minLength: minLength(6) }
}

const v$ = useVuelidate(rules, loginState)

const showPassword = ref(false)

function login() {
  if (v$.value.$invalid) return
  router.push('/game')
}
</script>

<template>
  <v-container class="mx-auto">
    <v-card min-width="400" color="#181818">
      <v-card-title color="white">Login</v-card-title>
      <v-card-text>
        <v-form @submit.prevent="login">
          <v-text-field
            v-model="loginState.email"
            label="Email"
            :error-messages="v$?.email?.$errors.map((e) => e.$message)"
            required
            @blur="v$.email.$touch"
            @input="v$.email.$touch"
          ></v-text-field>
          <v-text-field
            v-model="loginState.password"
            label="Password"
            :type="showPassword ? 'text' : 'password'"
            :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
            @click:append="showPassword = !showPassword"
            :error-messages="v$?.password?.$errors.map((e) => e.$message)"
            required
            @blur="v$.password.$touch"
            @input="v$.password.$touch"
          ></v-text-field>
          <v-btn type="submit" color="green">Login</v-btn>
        </v-form>
      </v-card-text>
    </v-card>
  </v-container>
</template>
