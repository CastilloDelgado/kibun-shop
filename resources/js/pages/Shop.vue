<script setup lang="ts">
import ShopLayout from '@/layouts/ShopLayout.vue';
import { Head } from '@inertiajs/vue3';

const photos = [
  { id: 1, alt: 'Playera Kibun verde en uso' },
  { id: 2, alt: 'Detalle del sello rojo de Kibun sobre tela oscura' },
  { id: 6, alt: 'Playera Kibun crema con estampado rojo' },
  { id: 7, alt: 'Detalle del estampado blanco sobre playera verde' },
  { id: 3, alt: 'Playera Kibun verde con estampado blanco' },
  { id: 8, alt: 'Detalle del estampado rojo sobre tela crema' },
  { id: 5, alt: 'Playera Kibun oscura con estampado blanco' },
  { id: 4, alt: 'Acercamiento a la textura del estampado blanco' },
];
</script>

<template>
  <Head title="Tienda" />
  <ShopLayout>
    <main class="shop-gallery flex-1" aria-label="Tienda — playeras Kibun">
      <div class="photo-scatter">
        <div class="collection-label">
          <h1>Última colección<br />de playeras Kibun</h1>
        </div>
        <figure v-for="(photo, index) in photos" :key="photo.id" class="scattered-photo">
          <img
            :src="`/images/tshirts/shirt-${photo.id}.jpeg`"
            :alt="photo.alt"
            :loading="index < 3 ? 'eager' : 'lazy'"
            decoding="async"
          />
        </figure>
      </div>
    </main>
  </ShopLayout>
</template>

<style scoped>
.shop-gallery {
  overflow: hidden;
  padding: 140px 0 32px;
}

.photo-scatter {
  position: relative;
  width: 100%;
  aspect-ratio: 1 / 1.12;
  margin: 0 auto;
}

.collection-label {
  position: absolute;
  z-index: 10;
  top: 24%;
  left: 5%;
  max-width: 420px;
  padding: clamp(24px, 3vw, 48px);
  background: #fff;
}

.collection-label h1 {
  margin: 0;
  font-size: clamp(24px, 3.2vw, 48px);
  font-weight: 500;
  line-height: 1.1;
  letter-spacing: -0.04em;
}

.scattered-photo {
  position: absolute;
  margin: 0;
}

.scattered-photo img {
  display: block;
  width: 100%;
  height: auto;
  max-height: 70vh;
  max-height: 70svh;
  object-fit: contain;
  object-position: top left;
}

/* Let the larger photographs extend beyond the sides of the page. */
.scattered-photo:nth-child(1) { left: -8%; top: 0; width: 35%; }
.scattered-photo:nth-child(2) { left: 43%; top: 3%; width: 16%; }
.scattered-photo:nth-child(3) { left: 80%; top: -3%; width: 35%; }
.scattered-photo:nth-child(4) { left: -4%; top: 49%; width: 22%; }
.scattered-photo:nth-child(5) { left: 33%; top: 31%; width: 35%; }
.scattered-photo:nth-child(6) { left: 87%; top: 46%; width: 25%; }
.scattered-photo:nth-child(7) { left: 20%; top: 73%; width: 28%; }
.scattered-photo:nth-child(8) { left: 66%; top: 77%; width: 19%; }

@media (max-width: 639px) {
  .shop-gallery {
    padding: 170px 0 32px;
  }

  .photo-scatter {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    align-items: start;
    gap: 20px 36px;
    aspect-ratio: auto;
    width: 112%;
    margin-left: -6%;
  }

  .collection-label {
    top: 9%;
    left: 10%;
    max-width: 78%;
    padding: 24px;
  }

  .scattered-photo:nth-child(n) {
    position: relative;
    top: auto;
    left: auto;
    width: 100%;
  }

  .scattered-photo:nth-child(even) {
    width: 88%;
    justify-self: end;
    margin-top: 20px;
  }

  .scattered-photo:nth-child(5) {
    width: 110%;
    justify-self: end;
  }
}
</style>
