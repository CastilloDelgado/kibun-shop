<script setup lang="ts">
import ShopLayout from '@/layouts/ShopLayout.vue';
import { Head } from '@inertiajs/vue3';
import { ChevronLeft, ChevronRight } from 'lucide-vue-next';
import { reactive } from 'vue';

const products = reactive([
  { title: 'Kibun Bosque', description: 'Verde profundo con gráfica blanca.', price: '$450 MXN', images: [1, 3, 7] },
  { title: 'Kibun Sello', description: 'Base oscura y un acento en rojo.', price: '$450 MXN', images: [2, 5, 4] },
  { title: 'Kibun Crema', description: 'Tono natural con estampado rojo.', price: '$480 MXN', images: [6, 8, 2] },
  { title: 'Kibun Trazo', description: 'Líneas orgánicas sobre verde.', price: '$450 MXN', images: [3, 7, 1] },
  { title: 'Kibun Noche', description: 'Gráfica blanca sobre fondo oscuro.', price: '$480 MXN', images: [5, 4, 2] },
  { title: 'Kibun Rojo', description: 'Un sello gráfico en tono cálido.', price: '$450 MXN', images: [8, 6, 2] },
  { title: 'Kibun Forma', description: 'Texturas y formas en contraste.', price: '$480 MXN', images: [4, 5, 7] },
  { title: 'Kibun Verde', description: 'Una pieza de la colección en verde.', price: '$450 MXN', images: [7, 1, 3] },
  { title: 'Kibun Estudio', description: 'Gráfica roja sobre una base clara.', price: '$500 MXN', images: [6, 2, 8] },
].map((product, index) => ({ ...product, id: index + 1, activeImage: 0 })));

function moveImage(product: (typeof products)[number], direction: number) {
  product.activeImage = (product.activeImage + direction + product.images.length) % product.images.length;
}

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
      <section class="photo-scatter" aria-labelledby="collection-heading">
        <div class="collection-label">
          <h1 id="collection-heading">Última colección<br />de playeras Kibun</h1>
        </div>
        <figure v-for="(photo, index) in photos" :key="photo.id" class="scattered-photo">
          <img
            :src="`/images/tshirts/shirt-${photo.id}.jpeg`"
            :alt="photo.alt"
            :loading="index < 3 ? 'eager' : 'lazy'"
            decoding="async"
          />
        </figure>
      </section>

      <section class="product-section" aria-labelledby="products-heading">
        <div class="product-heading">
          <h2 id="products-heading">Playeras Kibun</h2>
          <p>Gráfica para llevar contigo.</p>
        </div>

        <div class="product-grid">
          <article v-for="(product, index) in products" :key="product.id" class="product-card">
            <div class="product-carousel" role="group" :aria-label="`Imágenes de ${product.title}`" aria-roledescription="carrusel">
              <img
                :src="`/images/tshirts/shirt-${product.images[product.activeImage]}.jpeg`"
                :alt="`${product.title}, vista ${product.activeImage + 1} de ${product.images.length}`"
                :loading="index < 3 ? 'eager' : 'lazy'"
                decoding="async"
                class="product-image"
              />
              <button type="button" class="carousel-arrow carousel-arrow-previous" :aria-label="`Imagen anterior de ${product.title}`" @click="moveImage(product, -1)">
                <ChevronLeft :size="20" aria-hidden="true" />
              </button>
              <button type="button" class="carousel-arrow carousel-arrow-next" :aria-label="`Imagen siguiente de ${product.title}`" @click="moveImage(product, 1)">
                <ChevronRight :size="20" aria-hidden="true" />
              </button>
            </div>
            <div class="product-details">
              <h3>{{ product.title }}</h3>
              <p class="product-price">{{ product.price }}</p>
              <p class="product-description">{{ product.description }}</p>
            </div>
          </article>
        </div>
      </section>

    </main>
  </ShopLayout>
</template>

<style scoped>
.shop-gallery {
  overflow: hidden;
  padding: 140px 0 32px;
}

.product-section {
  width: 100%;
  max-width: 960px;
  margin: 0 auto;
  padding: 0 24px 112px;
}

.product-heading {
  max-width: 300px;
  margin: 0 auto 40px;
}

.product-heading h2 {
  margin: 0 0 12px;
  font-size: clamp(28px, 3.2vw, 48px);
  font-weight: 500;
  line-height: 1.1;
  letter-spacing: -0.04em;
}

.product-heading p {
  margin: 0;
  color: #666;
  font-size: 14px;
}

.product-grid {
  display: grid;
  max-width: 300px;
  margin: 0 auto;
  grid-template-columns: minmax(0, 1fr);
  gap: 48px 28px;
}

.product-card {
  min-width: 0;
}

.product-carousel {
  position: relative;
  aspect-ratio: 4 / 5;
  overflow: hidden;
  background: #f4f4f4;
}

.product-image {
  display: block;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.carousel-arrow {
  position: absolute;
  top: 50%;
  display: flex;
  width: 40px;
  height: 40px;
  align-items: center;
  justify-content: center;
  transform: translateY(-50%);
  border: 0;
  background: transparent;
  color: #fff;
  cursor: pointer;
  filter: drop-shadow(0 1px 2px rgb(0 0 0 / 35%));
  transition: transform 150ms ease;
}

.carousel-arrow:hover,
.carousel-arrow:focus-visible {
  transform: translateY(-50%) scale(1.2);
}

.carousel-arrow:focus-visible {
  outline: 2px solid #000;
  outline-offset: 3px;
}

.carousel-arrow-previous { left: 12px; }
.carousel-arrow-next { right: 12px; }

.product-details {
  display: grid;
  grid-template-columns: minmax(0, 1fr) auto;
  align-items: baseline;
  gap: 4px 12px;
  padding-top: 10px;
}

.product-details h3 {
  margin: 0;
  font-size: 14px;
  font-weight: 500;
  line-height: 1.35;
  letter-spacing: -0.02em;
}

.product-description {
  grid-column: 1 / -1;
  margin: 0;
  color: #666;
  font-size: 12px;
  line-height: 1.4;
}

.product-price {
  margin: 0;
  font-size: 12px;
  font-weight: 500;
  line-height: 1.35;
  white-space: nowrap;
}

@media (min-width: 640px) {
  .product-section { padding-right: 40px; padding-left: 40px; }
  .product-heading { max-width: none; }
  .product-grid { max-width: none; grid-template-columns: repeat(2, minmax(0, 1fr)); }
}

@media (min-width: 1024px) {
  .product-section { padding-right: 64px; padding-left: 64px; }
  .product-grid { grid-template-columns: repeat(3, minmax(0, 1fr)); }
}

.photo-scatter {
  position: relative;
  width: 100%;
  height: clamp(420px, 52vw, 640px);
  margin: 0 auto;
  mask-image: linear-gradient(to bottom, #000 55%, transparent 100%);
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
  filter: grayscale(1);
  transition: filter 300ms ease;
}

.scattered-photo img:hover {
  filter: grayscale(0);
}

@media (prefers-reduced-motion: reduce) {
  .scattered-photo img,
  .carousel-arrow {
    transition: none;
  }
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
    height: auto;
    max-height: 520px;
    overflow: hidden;
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
