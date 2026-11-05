<script setup lang="ts">
import { Link } from '@inertiajs/vue3';
</script>

<template>
  <footer class="flex h-16 shrink-0 items-center justify-center bg-black">
    <Link href="/" aria-label="Kibun, inicio">
      <img src="/favicon.png?v=2" alt="" width="32" height="32" class="h-8 w-8 object-contain" />
    </Link>
  </footer>
</template>
