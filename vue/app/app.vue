<script setup lang="ts">
import { signOut } from "firebase/auth";

const user = useCurrentUser();
const auth = useFirebaseAuth()!;

const handleSignOut = async () => {
  try {
    await signOut(auth);
  } catch (error) {
    console.error("Logout error:", error);
  }
};

useHead({
  meta: [{ name: "viewport", content: "width=device-width, initial-scale=1" }],
  link: [{ rel: "icon", href: "/favicon.ico" }],
  htmlAttrs: {
    lang: "en",
  },
});
</script>

<template>
  <UApp>
    <!-- Show auth form if not logged in -->
    <div v-if="!user" class="min-h-screen flex items-center justify-center p-4">
      <div class="w-full max-w-md">
        <AuthForm />
      </div>
    </div>

    <!-- Show main app if logged in -->
    <template v-else>
      <UHeader>
        <template #left>
          <NuxtLink to="/">
            <AppLogo class="w-auto h-6 shrink-0" />
          </NuxtLink>
        </template>

        <template #right>
          <div class="text-sm text-muted mr-4">
            {{ user.email }}
          </div>

          <UButton
            @click="handleSignOut"
            icon="i-lucide-log-out"
            aria-label="Sign Out"
            color="neutral"
            variant="ghost"
          >
            Sign Out
          </UButton>

          <UColorModeButton />
        </template>
      </UHeader>

      <UMain>
        <NuxtPage />
      </UMain>

      <USeparator icon="i-lucide-message-circle-question-mark" />

      <UFooter>
        <template #left>
          <p class="text-sm text-muted">
            daily-question.com • {{ new Date().getFullYear() }}
          </p>
        </template>

        <template #right>
          <UButton
            to="https://github.com/jensravn/daily-question"
            target="_blank"
            icon="i-simple-icons-github"
            aria-label="GitHub"
            color="neutral"
            variant="ghost"
          />
        </template>
      </UFooter>
    </template>
  </UApp>
</template>
