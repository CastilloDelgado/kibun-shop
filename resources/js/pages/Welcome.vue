<script setup lang="ts">
import ShopLayout from "@/layouts/ShopLayout.vue";
import { Head } from "@inertiajs/vue3";
import { useMediaQuery } from "@vueuse/core";
import { computed } from "vue";

const artworks = Array.from({ length: 16 }, (_, index) => index + 1)
  .filter((number) => number !== 5)
  .map((number) => {

  return {
    src: `/images/art/artwork-${number}.png`,
    alt: `Obra gráfica Kibun ${number}`,
  };
});

for (let index = artworks.length - 1; index > 0; index--) {
  const randomIndex = Math.floor(Math.random() * (index + 1));
  [artworks[index], artworks[randomIndex]] = [
    artworks[randomIndex],
    artworks[index],
  ];
}

const isDesktop = useMediaQuery("(min-width: 1024px)");
const isTablet = useMediaQuery("(min-width: 640px)");
const columns = computed(() => isDesktop.value ? 5 : isTablet.value ? 3 : 2);
const rotationChoices = artworks.map(() => Math.random());
const rotatingIndices = computed(() => {
  const selected = new Set<number>();

  for (let start = 0; start < artworks.length; start += columns.value) {
    const end = Math.min(start + columns.value, artworks.length);
    let chosen = start;

    for (let index = start + 1; index < end; index++) {
      if (rotationChoices[index] < rotationChoices[chosen]) chosen = index;
    }

    selected.add(chosen);
  }

  return selected;
});
</script>

<template>
  <Head title="Inicio" />
  <ShopLayout>

    <main
      id="arte"
      aria-label="Galería de arte"
      class="flex flex-1 flex-col justify-center scroll-mt-24 px-6 pb-24 pt-24 sm:px-10 lg:px-16"
    >
      <div
        class="grid grid-cols-2 items-start gap-3 sm:grid-cols-3 sm:gap-5 lg:grid-cols-5"
      >
        <figure
          v-for="(artwork, index) in artworks"
          :key="index"
          class="m-0 aspect-square overflow-hidden bg-white grayscale transition-[filter] duration-300 hover:invert motion-reduce:transition-none"
        >
          <img
            :src="artwork.src"
            :alt="artwork.alt"
            :loading="index < 5 ? 'eager' : 'lazy'"
            decoding="async"
            class="block h-full w-full object-contain object-center"
            :class="{ 'artwork-spin': rotatingIndices.has(index) }"
            :style="rotatingIndices.has(index) ? {
              animationDuration: `${70 + (Math.floor(index / columns) % 3) * 10}s`,
              animationDirection: Math.floor(index / columns) % 2 ? 'reverse' : 'normal',
            } : undefined"
          />
        </figure>
      </div>
    </main>

  </ShopLayout>
</template>

<style scoped>
.artwork-spin {
  animation: artwork-rotation 70s linear infinite;
}

@keyframes artwork-rotation {
  from {
    transform: scale(0.7) rotate(0deg);
  }
  to {
    transform: scale(0.7) rotate(360deg);
  }
}

@media (prefers-reduced-motion: reduce) {
  .artwork-spin {
    animation: none;
  }
}
</style>
