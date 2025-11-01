<script setup lang="ts">
interface Props {
  question: string;
  options: string[];
  selectedOption?: string;
  disabled?: boolean;
}

const props = withDefaults(defineProps<Props>(), {
  selectedOption: undefined,
  disabled: false,
});

const emit = defineEmits<{
  select: [optionId: string];
}>();

const handleOptionSelect = (optionId: string) => {
  if (!props.disabled) {
    emit("select", optionId);
  }
};
</script>

<template>
  <UCard>
    <div class="space-y-6">
      <!-- Question -->
      <div>
        <h2 class="text-2xl font-semibold">{{ question }}</h2>
      </div>

      <!-- Options -->
      <div class="space-y-3">
        <button
          v-for="option in options"
          :key="option.id"
          type="button"
          :disabled="disabled"
          class="w-full text-left p-4 rounded-lg border-2 transition-all duration-200"
          :class="[
            selectedOption === option.id
              ? 'border-primary bg-primary/10'
              : 'border-gray-200 dark:border-gray-700 hover:border-primary/50 hover:bg-gray-50 dark:hover:bg-gray-800',
            disabled ? 'opacity-50 cursor-not-allowed' : 'cursor-pointer',
          ]"
          @click="handleOptionSelect(option.id)"
        >
          <div class="flex items-center gap-3">
            <!-- Radio indicator -->
            <div
              class="w-5 h-5 rounded-full border-2 flex items-center justify-center shrink-0"
              :class="[
                selectedOption === option.id
                  ? 'border-primary'
                  : 'border-gray-300 dark:border-gray-600',
              ]"
            >
              <div
                v-if="selectedOption === option.id"
                class="w-3 h-3 rounded-full bg-primary"
              />
            </div>

            <!-- Option text -->
            <span class="text-base">{{ option }}</span>
          </div>
        </button>
      </div>
    </div>
  </UCard>
</template>
