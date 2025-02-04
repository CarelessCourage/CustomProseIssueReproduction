<script setup lang="ts">
const route = useRoute()

const { data: page } = await useAsyncData('page-' + route.path, () => {
  return queryCollection('content').path(route.path).first()
})

if (!page.value) {
  throw createError({ statusCode: 404, statusMessage: 'Page not found', fatal: true })
}

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
