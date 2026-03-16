<script lang="ts">
import { defineComponent } from "vue";
import type { Category } from "@shared/models/Category";
import type { Product } from "@shared/models/Product";
import type { CartItem } from "@shared/models/CartItem";
import { Cart } from "@shared/classes/Cart";
import ProductCard from "./components/ProductCard.vue";

export default defineComponent({
  name: "App",
  components: { ProductCard },
  data() {
    const instrumentos: Category = { id: 1, title: "Instrumentos Musicais" };
    const roupas: Category = { id: 2, title: "Roupas" };
    const livros: Category = { id: 3, title: "Livros" };

    const products: Product[] = [
      {
        id: 1,
        name: "Guitarra",
        price: 400,
        category: instrumentos,
      },
      {
        id: 2,
        name: "Camiseta",
        price: 100,
        category: roupas,
      },
      {
        id: 3,
        name: "Livro de TypeScript",
        price: 80,
        category: livros,
      },
      {
        id: 4,
        name: "Violão",
        price: 350,
        category: instrumentos,
      },
    ];

    const cart = new Cart();
    const cartItems: CartItem[] = [];

    return {
      products,
      cart,
      cartItems,
    };
  },

  methods: {
    formatBRL(value: number): string {
      return new Intl.NumberFormat("pt-BR", {
        style: "currency",
        currency: "BRL",
      }).format(value);
    },

    syncCartItems(): void {
      this.cartItems.length = 0;
      this.cartItems.push(...this.cart.getItems());
    },

    addToCart(product: Product): void {
      this.cart.addItem(product, 1);
      this.syncCartItems();
    },

    increaseQuantity(productId: number): void {
      this.cart.increaseQuantity(productId);
      this.syncCartItems();
    },

    decreaseQuantity(productId: number): void {
      this.cart.decreaseQuantity(productId);
      this.syncCartItems();
    },

    removeItem(productId: number): void {
      this.cart.removeItem(productId);
      this.syncCartItems();
    }
  }
});
</script>

<template>
  <div class="app">
    <header class="app-header">
      <h1>E-commerce com Vue.js & Options API</h1>
    </header>

    <section class="app-products">
      <h2>Produtos</h2>
      <div class="product-grid">
        <ProductCard
          v-for="product in products"
          :key="product.id"
          :product="product"
          :priceBR="formatBRL(product.price)"
          @add-to-cart="addToCart(product)"
        />
      </div>
    </section>

    <aside class="app-cart">
      <h2>Carrinho</h2>
      
      <p v-if="cartItems.length === 0" class="cart-stats">Seu carrinho está vazio!</p>
      
      <div v-else>
        <p class="cart-stats">
          <strong>Total de itens:</strong> {{ cart.getTotalItems() }}
        </p>
        <p class="cart-stats">
          <strong>Valor total:</strong> {{ formatBRL(cart.getFinalPrice()) }}
        </p>

      <div class="cart-list">
        <h3>Itens no carrinho</h3>
        <ul class="cart-list-items">
          <li
            v-for="item in cartItems"
            :key="item.product.id"
            class="cart-list-item"
          >
            <span class="cart-list-label">
              {{ item.product.name }} × {{ item.quantity }}
            </span>
            <span class="cart-item-price">
              {{ formatBRL(item.product.price * item.quantity) }}
            </span>
            <div class="cart-list-actions">
              <button
                type="button"
                class="btn btn-small"
                title="Remover quantidade"
                @click="decreaseQuantity(item.product.id)"
              >
                −
              </button>
              <span class="quantity">
                {{ item.quantity }}
              </span>
              <button
                type="button"
                class="btn btn-small"
                title="Adicionar quantidade"
                @click="increaseQuantity(item.product.id)"
              >
                +
              </button>
              <button
                type="button"
                class="btn btn-small btn-danger"
                title="Excluir item"
                @click="removeItem(item.product.id)"
              >
                Excluir
              </button>
            </div>
          </li>
        </ul>
      </div>
     </div>
    </aside>
  </div>
</template>
