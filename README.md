# Reactive Layouts

This is a starter project that uses `@vueuse/core` to create dynamic layouts based on the user's screensize.

## How exactly ?
1. Create the various `layouts` in the `/layouts directory`. In our case, we have `desktop.vue` that represents the desktop layout, `tablet.vue` for tablet layout and `mobile.vue` for mobile layout.

2. Use `useMediaQuery` to identify various breakpoints. The returned breakpoint are valid `ref<boolean>` that we can use to dynamicaly switch between the layout.

```typescript
import { useMediaQuery} from '@vueuse/core';

const layout = ref('')

const isLargeScreen = useMediaQuery('(min-width: 1024px)');
const isMediumScreen = useMediaQuery('(min-width: 768px)');
```

3. Use `watchEffect()` to track a change in either breakpoints. This is useful for a case where a user switches between desktop/tablet/mobile on the same browser window.

```typescript
watchEffect(() => {
  updateLayout(isMediumScreen.value, isLargeScreen.value);
})
```

4. The actual layout switch

```typescript
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
```

5. Bind the layout value to the `NuxtLayout`

```html
<template>
  <NuxtLayout :name="layout">
    <NuxtPage />
  </NuxtLayout>
</template>
```


## Running Locally

After cloning/downloading the source files

npm - `npm install`. Yarn - `yarn install`

npm- `npm run dev -o`. Yarn - `yarn dev -o`

Navigate to `http://localhost:3000/dashboard`

