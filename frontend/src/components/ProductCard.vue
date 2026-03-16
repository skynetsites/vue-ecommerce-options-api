<script setup lang="ts">
import type { Product } from "@shared/models/Product";

defineProps<{
  product: Product;
  priceBR: string;
}>();

const emit = defineEmits<{
  (e: "add-to-cart"): void;
}>();
</script>

<template>
  <article class="product-card">
    <h3 class="product-card-name">{{ product.name }}</h3>
    <p class="product-card-price">{{ priceBR }}</p>
    <p class="product-card-category">{{ product.category.title }}</p>
    <button type="button" class="product-card-btn" @click="emit('add-to-cart')">
      Adicionar
    </button>
  </article>
</template>