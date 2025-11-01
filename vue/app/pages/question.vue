<script setup lang="ts">
import { ref } from "vue";

interface Option {
  id: string;
  text: string;
}

const question = ref("What is your preferred programming language?");
const options = ref<Option[]>([
  { id: "1", text: "TypeScript" },
  { id: "2", text: "JavaScript" },
  { id: "3", text: "Python" },
  { id: "4", text: "Go" },
]);

const selectedOption = ref<string>();
const isSubmitted = ref(false);

const handleSelect = (optionId: string) => {
  selectedOption.value = optionId;
};

const handleSubmit = () => {
  if (selectedOption.value) {
    isSubmitted.value = true;
  }
};

const handleReset = () => {
  selectedOption.value = undefined;
  isSubmitted.value = false;
};

const getSelectedOptionText = () => {
  const option = options.value.find((opt) => opt.id === selectedOption.value);
  return option?.text || "";
};
</script>

<template>
  <div class="container max-w-2xl mx-auto py-8 px-4">
    <div class="space-y-6">
      <!-- Header -->
      <div class="text-center">
        <h1 class="text-4xl font-bold">Daily Question</h1>
        <p class="text-muted mt-2">Answer today's question</p>
      </div>

      <!-- Question Card -->
      <QuestionCard
        :question="question"
        :options="options"
        :selected-option="selectedOption"
        :disabled="isSubmitted"
        @select="handleSelect"
      />

      <!-- Submit Button -->
      <div v-if="!isSubmitted" class="flex justify-center">
        <UButton :disabled="!selectedOption" size="xl" @click="handleSubmit">
          Submit Answer
        </UButton>
      </div>

      <!-- Result -->
      <UCard v-if="isSubmitted" class="bg-primary/10">
        <div class="text-center space-y-4">
          <div>
            <UIcon name="i-lucide-check-circle" class="text-primary text-5xl" />
          </div>
          <div>
            <h3 class="text-xl font-semibold">Answer Submitted!</h3>
            <p class="text-muted mt-2">
              You selected:
              <span class="font-semibold text-primary">{{
                getSelectedOptionText()
              }}</span>
            </p>
          </div>
          <UButton variant="subtle" @click="handleReset">
            Answer Again
          </UButton>
        </div>
      </UCard>
    </div>
  </div>
</template>
