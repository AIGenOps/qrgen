<script setup lang="ts">
import { useI18n } from 'vue-i18n'

const { t } = useI18n()
const hideCredits = ['1', 'true'].includes((import.meta.env.VITE_HIDE_CREDITS ?? '').toLowerCase())
</script>

<template>
  <footer
    v-if="!hideCredits"
    class="fixed inset-x-0 bottom-0 hidden p-4 text-sm text-zinc-600 dark:text-zinc-400 md:flex md:justify-center"
  >
    <div class="flex items-center gap-2">
      <span>{{ t('Created by') }}</span>
      <a
        href="https://github.com/AIGenOps"
        target="_blank"
        class="text-zinc-900 hover:text-zinc-700 dark:text-zinc-100 dark:hover:text-zinc-300"
        >AIGenOps</a
      >
    </div>
  </footer>
</template>

<style scoped>
footer {
  background: rgba(255, 255, 255, 0.8);
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
}

.dark footer {
  background: rgba(24, 24, 27, 0.8);
}
</style>
