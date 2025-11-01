<template>
  <div>
    <UPageHero
      title="Daily Question"
      description="Answer a new question every day and share your thoughts with the community."
      :links="[
        {
          label: 'Answer Today\'s Question',
          to: '/question',
          trailingIcon: 'i-lucide-arrow-right',
          size: 'xl',
        },
        {
          label: 'View on GitHub',
          to: 'https://github.com/jensravn/daily-question',
          target: '_blank',
          icon: 'i-simple-icons-github',
          size: 'xl',
          color: 'neutral',
          variant: 'subtle',
        },
      ]"
    />

    <UPageSection
      id="features"
      title="How it works"
      description="A simple and engaging way to share your opinions and connect with others."
      :features="[
        {
          icon: 'i-lucide-message-circle-question',
          title: 'Daily Questions',
          description:
            'Answer a new thought-provoking question every day. Each question is designed to spark interesting conversations.',
        },
        {
          icon: 'i-lucide-users',
          title: 'Community Insights',
          description:
            'See how others answered and compare your perspective with the community. Discover different viewpoints.',
        },
        {
          icon: 'i-lucide-trophy',
          title: 'Track Your Progress',
          description:
            'Keep a history of all your answers and watch your participation grow over time.',
        },
        {
          icon: 'i-lucide-shield-check',
          title: 'Secure & Private',
          description:
            'Your account is protected with Firebase Authentication. Your data is safe and secure.',
        },
      ]"
    />

    <UPageSection>
      <UPageCTA
        title="Ready to share your thoughts?"
        description="Join the conversation and answer today's question. Sign in to get started."
        variant="subtle"
        :links="[
          {
            label: 'Answer Today\'s Question',
            to: '/question',
            trailingIcon: 'i-lucide-arrow-right',
            color: 'neutral',
          },
        ]"
      />
    </UPageSection>
  </div>
</template>
