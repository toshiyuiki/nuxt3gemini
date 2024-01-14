<template>
  <div class="the-base">
    <slot />
  </div>
</template>

<script lang="ts" setup>
  useJsonld({
    '@context': 'https://schema.org',
    '@type': 'Thing',
    name: 'static json',
  });
</script>

<style lang="scss">
  .the-base{
  }
</style>
