<script setup lang="ts">
import { signOut } from "firebase/auth";
import AuthForm from "../components/AuthForm.vue";

const user = useCurrentUser();
const auth = useFirebaseAuth()!;

const handleLogout = async () => {
  try {
    await signOut(auth);
  } catch (error) {
    console.error("Logout error:", error);
  }
};
</script>

<template>
  <UApp>
    <NuxtRouteAnnouncer />

    <!-- Show auth form when not logged in -->
    <AuthForm v-if="!user" />

    <!-- Show main content when logged in -->
    <div v-else>
      <h1>Welcome, {{ user.email }}</h1>
      <button @click="handleLogout">Logout</button>

      <p>You are successfully logged in!</p>
      <p>This is where your daily question feature will go.</p>
    </div>
  </UApp>
</template>
