<script setup></script>

<template>
  <RouterLink
    :to="{
      name: 'get-view',
      params: { id: 1 },
      query: { search: 'show', page: 1 },
    }"
  >
    <div>Go to id : 1</div>
  </RouterLink>
</template>

<style scoped></style>
