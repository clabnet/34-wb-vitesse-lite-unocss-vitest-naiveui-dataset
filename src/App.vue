<script setup lang="ts">
import { getNaiveThemeProps, lang_storage } from '@/composables'
import themeOverrides from '~/naive-ui-theme-overrides.json'
import { useAppStore } from '@/stores/app'

const htmlEl = document.documentElement
const headerHeight = toRef(useAppStore(), 'headerHeight')

const { locale } = useI18n()
useHead({
  title: 'Vue3 workbench',
  meta: [{ name: 'description', content: 'Study vue3 api' }],
})

useCssVar('--app-primary-color', htmlEl).value = themeOverrides.common.primaryColor
const heightRef = useCssVar('--app-header-height', htmlEl)
watchEffect(() => {
  locale.value = lang_storage.value
  heightRef.value = `${headerHeight.value}px`
})
</script>

<template>
  <n-config-provider v-bind="getNaiveThemeProps">
    <n-message-provider>
      <router-view />
    </n-message-provider>
  </n-config-provider>
</template>
