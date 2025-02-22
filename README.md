# Custom Prose Breaks in the MDC component

When I create my own prose components they work fine if I use a markdown file  and the regular ContentRenderer in nuxt content, but if I store the markdown in a variable and insert it into the MDC component - not only does my custom prose components not show up, the default prose component breaks. But this only happens in the MDC component, while the ContentRenderer component works as expected. It seems MDC will literally render a ProseH1 element into the browsers HTML instead of a h1 element in this case. 

I have made a reproduction and tried to keep it as simple and clear as possible. 

Reproduction: [CustomProseIssueReproduction](https://github.com/CarelessCourage/CustomProseIssueReproduction/tree/content)

<img width="231" alt="Screenshot 2025-02-22 at 15 17 01" src="https://github.com/user-attachments/assets/84b53e2b-e97d-478a-96d5-d22dfb5b8584" />

```vue
<script setup lang="ts">
const route = useRoute()

const { data: page } = await useAsyncData('page-' + route.path, () => {
  return queryCollection('content').path(route.path).first()
})

const md = `
# This should be an h1 element and it should have the "custom prose" prefix from the custom ProseH1 component but its a proseh1 element and it lacks the custom prose text
`
</script>

<template>
  <!-- Works as expected -->
  <ContentRenderer v-if="page":value="page" />

  <!-- Does not work as expected -->
  <MDC :value="md" tag="article" />
</template>
```
