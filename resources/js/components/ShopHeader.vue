<script setup lang="ts">
import { Link } from "@inertiajs/vue3";
</script>

<template>
  <header
      class="fixed inset-x-0 top-0 z-50 flex items-center justify-between flex-wrap gap-5 bg-white/95 px-6 py-7 sm:px-10 lg:px-16"
    >
      <Link
        href="/"
        class="inline-flex shrink-0 items-center gap-4 text-2xl uppercase font-semibold tracking-tight"
        aria-label="Kibun, inicio"
      >
        <span>kibun</span>
        <img
          src="/favicon.png?v=2"
          alt=""
          width="32"
          height="32"
          class="h-8 w-8 object-contain"
        />
      </Link>

      <nav
        aria-label="Navegación principal"
        class="flex items-center flex-wrap gap-5 text-sm sm:gap-9"
      >
        <Link href="/" class="header-link focus-visible:outline-offset-4">Inicio</Link>
        <a
          href="/#arte"
          class="header-link capitalize focus-visible:outline-offset-4"
          >Arte</a
        >
        <Link
          href="/tienda"
          class="header-link capitalize focus-visible:outline-offset-4"
          >Tienda</Link
        >
        <a
          href="/#tattoo"
          class="header-link capitalize focus-visible:outline-offset-4"
          >Tattoo</a
        >
        <a
          href="/#contacto"
          class="header-link capitalize focus-visible:outline-offset-4"
          >contacto</a
        >
      </nav>
    </header>
</template>

<style scoped>
.header-link {
  position: relative;
  color: #000;
}

.header-link::after {
  content: '';
  position: absolute;
  right: 0;
  bottom: -4px;
  left: 0;
  height: 1px;
  background-color: currentColor;
  transform: scaleX(0);
  transform-origin: left;
  transition: transform 250ms ease;
}

.header-link:hover::after,
.header-link:focus-visible::after {
  transform: scaleX(1);
}


@media (prefers-reduced-motion: reduce) {
  .header-link::after { transition: none; }
}
</style>
