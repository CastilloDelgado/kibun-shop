<script setup lang="ts">
import ShopFooter from '@/components/ShopFooter.vue';
import ShopHeader from '@/components/ShopHeader.vue';
</script>

<template>
  <div class="flex min-h-dvh flex-col bg-white text-black">
    <ShopHeader />
    <slot />
    <ShopFooter />
  </div>
</template>
