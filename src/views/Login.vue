<template>
  <div class="login-page">
    <div class="container">
      <h2>Login to Your Portfolio</h2>
      <form @submit.prevent="handleLogin" class="login-form">
        <input
          v-model.trim="username"
          type="text"
          placeholder="Username"
          required
        />
        <input
          v-model.trim="password"
          type="password"
          placeholder="Password"
          required
        />
        <button type="submit">Login</button>
        <p v-if="error" class="error">{{ error }}</p>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const username = ref('')
const password = ref('')
const error = ref('')

// Optional: clear error on input change
watch([username, password], () => {
  error.value = ''
})

const handleLogin = () => {
  const validUser = 'admin'
  const validPass = '1234'

  if (
    username.value.toLowerCase() === validUser &&
    password.value === validPass
  ) {
    localStorage.setItem('loggedIn', 'true')
    router.push('/')
  } else {
    error.value = 'Invalid username or password.'
  }
}
</script>

<style scoped>
.login-page {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  padding-top: 80px;
  min-height: 100vh;
  background-color: #f3f4f6;
}

.container {
  background-color: #ffffff;
  padding: 50px;
  border-radius: 12px;
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.1);
  width: 100%;
  max-width: 500px;
  font-size: 18px;
}

.login-form {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.login-form input {
  padding: 14px;
  border-radius: 6px;
  border: 1px solid #ccc;
  font-size: 16px;
}

.login-form button {
  background-color: #3b82f6;
  color: white;
  padding: 14px;
  border: none;
  border-radius: 6px;
  font-size: 16px;
  cursor: pointer;
}

.login-form button:hover {
  background-color: #2563eb;
}

.error {
  color: red;
  text-align: center;
  font-weight: bold;
}
</style>
