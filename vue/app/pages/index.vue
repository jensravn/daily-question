<script setup lang="ts">
import { doc } from "firebase/firestore";
import { computed, ref, watch } from "vue";
import { useDocument, useFirestore } from "vuefire";

interface Option {
  id: string;
  text: string;
}

interface Question {
  question: string;
  options: string[];
}

const db = useFirestore()!;

const topicId = "LskYjWe3SaDIPd5B69a6";
const questionId = "q8cUeqS2b8VgASKhLj19";

const questionDocRef = doc(db, "topics", topicId, "questions", questionId);
const questionData = useDocument<Question>(questionDocRef);

const isLoading = ref(true);
const hasError = ref(false);
const errorMessage = ref("");

watch(
  questionData,
  (newData) => {
    isLoading.value = false;
    if (newData === null) {
      hasError.value = true;
      errorMessage.value =
        "Permission denied. Please check Firestore security rules.";
    }
  },
  { immediate: true }
);

const question = computed(
  () => questionData.value?.question || "Loading question..."
);
const options = computed(() => questionData.value?.options || []);

const selectedOption = ref<string>();
const selectedOptions = ref<string[]>([]);
const isSubmitted = ref(false);
</script>

<template>
  <div class="container max-w-2xl mx-auto py-8 px-4">
    <div class="space-y-6">
      <!-- Header -->
      <div class="text-center">
        <h1 class="text-4xl font-bold">Daily Question</h1>
        <p class="text-muted mt-2">Answer today's question</p>
      </div>

      <!-- Error state -->
      <UCard v-if="hasError" class="border-2 border-red-500">
        <div class="space-y-4">
          <div class="flex items-start gap-3">
            <UIcon
              name="i-lucide-alert-circle"
              class="text-red-500 text-2xl shrink-0 mt-1"
            />
            <div>
              <h3 class="text-lg font-semibold text-red-600">Error</h3>
              <p class="text-muted mt-1">{{ errorMessage }}</p>
            </div>
          </div>
        </div>
      </UCard>

      <QuestionCard
        v-else-if="options.length > 0"
        :question="question"
        :options="options"
        v-model="selectedOption"
        :disabled="isSubmitted"
      />

      <div
        v-if="!isSubmitted && options.length > 0"
        class="flex justify-center"
      >
        <UButton :disabled="selectedOptions.length === 0" size="xl">
          Submit Answer
        </UButton>
      </div>
    </div>
  </div>
</template>
