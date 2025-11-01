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
  <div class="space-y-6">
    <div class="text-center">
      <h1 class="text-3xl font-bold">Daily Question</h1>
      <p class="text-sm text-muted mt-2">
        {{ isLogin ? "Sign in to your account" : "Sign up to get started" }}
      </p>
    </div>

    <UCard>
      <form @submit.prevent="handleSubmit" class="space-y-4">
        <UFormField label="Email" name="email" required>
          <UInput
            v-model="email"
            type="email"
            placeholder="Enter your email"
            :disabled="loading"
            icon="i-lucide-mail"
            size="lg"
          />
        </UFormField>

        <UFormField label="Password" name="password" required>
          <UInput
            v-model="password"
            type="password"
            placeholder="Enter your password"
            :disabled="loading"
            icon="i-lucide-lock"
            size="lg"
          />
        </UFormField>

        <UAlert
          v-if="error"
          color="red"
          variant="subtle"
          :title="error"
          icon="i-lucide-alert-circle"
        />

        <UButton
          type="submit"
          :disabled="loading"
          :loading="loading"
          block
          size="lg"
        >
          {{ isLogin ? "Sign In" : "Create Account" }}
        </UButton>
      </form>
    </UCard>

    <div class="text-center">
      <UButton
        @click="toggleMode"
        :disabled="loading"
        variant="ghost"
        color="neutral"
      >
        {{
          isLogin
            ? "Need an account? Sign up"
            : "Already have an account? Sign in"
        }}
      </UButton>
    </div>
  </div>
</template>
