<script lang="ts" setup>
import { useMediaQuery} from '@vueuse/core';

const isLargeScreen = useMediaQuery('(min-width: 1024px)');
const isMediumScreen = useMediaQuery('(min-width: 768px)');

const layout = ref('');
// use this to update the layout
const updateLayout = (mediumScreen?: boolean, largeSreen?: boolean) => {
  switch (true) {
    case mediumScreen && !largeSreen:
      layout.value = 'tablet'
      break;
    case largeSreen:
      layout.value = 'desktop';
      break;
    default:
      layout.value = 'mobile'
      break;
  }
}
watchEffect(() => {
  updateLayout(isMediumScreen.value, isLargeScreen.value);
})

</script>
<template>
  <NuxtLayout :name="layout">
    <NuxtPage />
  </NuxtLayout>
</template>
