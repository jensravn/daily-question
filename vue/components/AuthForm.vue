<script setup lang="ts">
import { ref } from "vue";
import {
  signInWithEmailAndPassword,
  createUserWithEmailAndPassword,
} from "firebase/auth";

const auth = useFirebaseAuth()!;

const email = ref("");
const password = ref("");
const isLogin = ref(true);
const loading = ref(false);
const error = ref("");

const toggleMode = () => {
  isLogin.value = !isLogin.value;
  error.value = "";
};

const handleSubmit = async () => {
  error.value = "";
  loading.value = true;

  try {
    if (isLogin.value) {
      await signInWithEmailAndPassword(auth, email.value, password.value);
    } else {
      await createUserWithEmailAndPassword(auth, email.value, password.value);
    }
    // Clear form after successful auth
    email.value = "";
    password.value = "";
  } catch (err: any) {
    // Handle Firebase auth errors
    if (err.code === "auth/email-already-in-use") {
      error.value = "Email already in use. Try logging in instead.";
    } else if (err.code === "auth/invalid-email") {
      error.value = "Invalid email address.";
    } else if (err.code === "auth/weak-password") {
      error.value = "Password should be at least 6 characters.";
    } else if (err.code === "auth/user-not-found") {
      error.value = "No account found with this email.";
    } else if (err.code === "auth/wrong-password") {
      error.value = "Incorrect password.";
    } else if (err.code === "auth/invalid-credential") {
      error.value = "Invalid email or password.";
    } else {
      error.value = err.message || "An error occurred. Please try again.";
    }
  } finally {
    loading.value = false;
  }
};
</script>

<template>
  <div class="auth-container">
    <div class="auth-card">
      <h1>{{ isLogin ? "Login" : "Sign Up" }}</h1>

      <form @submit.prevent="handleSubmit">
        <div class="form-group">
          <label for="email">Email</label>
          <input
            id="email"
            v-model="email"
            type="email"
            required
            placeholder="Enter your email"
            :disabled="loading"
          />
        </div>

        <div class="form-group">
          <label for="password">Password</label>
          <input
            id="password"
            v-model="password"
            type="password"
            required
            placeholder="Enter your password"
            minlength="6"
            :disabled="loading"
          />
        </div>

        <div v-if="error" class="error-message">
          {{ error }}
        </div>

        <button type="submit" :disabled="loading" class="submit-btn">
          {{ loading ? "Processing..." : isLogin ? "Login" : "Sign Up" }}
        </button>
      </form>

      <div class="toggle-mode">
        <button @click="toggleMode" :disabled="loading" class="link-btn">
          {{
            isLogin
              ? "Need an account? Sign up"
              : "Already have an account? Login"
          }}
        </button>
      </div>
    </div>
  </div>
</template>
