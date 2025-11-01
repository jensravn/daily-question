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
    <div>
      <NuxtRouteAnnouncer />

      <!-- Show auth form when not logged in -->
      <AuthForm v-if="!user" />

      <!-- Show main content when logged in -->
      <div v-else class="app-content">
        <div class="header">
          <h1>Welcome, {{ user.email }}</h1>
          <button @click="handleLogout" class="logout-btn">Logout</button>
        </div>

        <div class="main-content">
          <p>You are successfully logged in!</p>
          <p>This is where your daily question feature will go.</p>
        </div>
      </div>
    </div>
  </UApp>
</template>
