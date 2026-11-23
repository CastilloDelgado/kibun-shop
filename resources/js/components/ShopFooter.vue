<script setup lang="ts">
import { Link } from '@inertiajs/vue3';
</script>

<template>
  <footer id="contacto" class="flex shrink-0 flex-col items-center justify-between gap-5 bg-black px-6 py-6 text-white sm:flex-row sm:px-10 lg:px-16">
    <Link href="/" aria-label="Kibun, inicio">
      <img src="/favicon.png?v=2" alt="" width="32" height="32" class="h-8 w-8 object-contain" />
    </Link>
    <div class="flex flex-col items-center gap-3 text-sm sm:flex-row sm:gap-6">
      <a
        href="https://www.instagram.com/kibuntattoo/"
        target="_blank"
        rel="noopener noreferrer"
        aria-label="Instagram de Kibun: @kibuntattoo (abre en una pestaña nueva)"
        class="hover:underline focus-visible:outline-offset-4"
      >
        Instagram @kibuntattoo
      </a>
      <a href="mailto:kibuntattoo@gmail.com" class="hover:underline focus-visible:outline-offset-4">
        kibuntattoo@gmail.com
      </a>
    </div>
  </footer>
</template>
