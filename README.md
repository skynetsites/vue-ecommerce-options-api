# E-commerce com Vue.js & Options API – Sistema de Carrinho de Compras

![TypeScript](https://img.shields.io/badge/TypeScript-5-blue?logo=typescript)
![Vue.js](https://img.shields.io/badge/Vue.js-3-green?logo=vue.js)
![Vite](https://img.shields.io/badge/Vite-6-646CFF?logo=vite)
![Status](https://img.shields.io/badge/status-estudo-blue)
![License](https://img.shields.io/badge/license-MIT-green)

## Descrição do projeto

Este projeto implementa uma **simulação de e-commerce** utilizando **TypeScript, POO e Vue.js**.

A aplicação é dividida em duas partes:

1. **Backend (Node + TypeScript)**  
   Implementa a lógica de negócio utilizando **Programação Orientada a Objetos**, incluindo models (`Category`, `Product`, `CartItem`) e a classe `Cart` responsável por gerenciar os itens do carrinho.

2. **Frontend (Vue.js + Options API)**  
   Interface que permite visualizar produtos, adicionar itens ao carrinho e acompanhar o resumo do pedido (total de unidades e valor total).

O objetivo é estudar **tipagem forte**, **POO**, **organização de código** e **Vue.js com Options API** em um cenário próximo de um sistema real.

# Preview

Interface simples de e-commerce demonstrando:

- Listagem de produtos
- Adição ao carrinho
- Cálculo automático do total
- Controle de quantidade
- Remoção de itens

# Estrutura do projeto

```
vue-ecommerce-options-api/
├── frontend/ 
│   ├── src/
│   │   ├── components/
│   │   │   └── ProductCard.vue
│   │   ├── App.vue
│   │   ├── main.ts
│   │   └── vite-env.d.ts
│   ├── index.html
│   ├── package.json
│   ├── tsconfig.json
│   └── vite.config.ts
├── src/
│   ├── classes/
│   │   ├── Cart.ts
│   │   └── User.ts
│   ├── models/
│   │   ├── CartItem.ts
│   │   ├── Category.ts
│   │   └── Product.ts
│   └── index.ts
├── .gitignore
├── LICENSE
├── package-lock.json
├── package.json
├── README.md
└── tsconfig.json
```

# Tecnologias utilizadas

- **TypeScript** (tipagem forte, sem `any`)
- **Node.js** (execução do exemplo em `src/index.ts`)
- **Vue 3** (Options API: `data`, `methods`, `props`)
- **Vite** (build e dev do frontend)
- **POO** (classes `Cart` e `User`; interfaces Category, Product, CartItem)

# Lógica do carrinho de compras

**A classe Cart gerencia os produtos adicionados:**

```ts
class Cart {
  private items: CartItem[] = [];

  addItem(product: Product, quantity: number): void { /* adiciona produto ou aumenta quantidade */ }
  getTotalItems(): number { /* retorna o total de unidades */ }
  getFinalPrice(): number { /* calcula o valor total do carrinho */ }
  getItems(): CartItem[] { /* retorna os itens do carrinho */ }
  decreaseQuantity(productId: number): void { /* diminui a quantidade ou remove se chegar a 0 */ }
  increaseQuantity(productId: number): void { /* aumenta a quantidade do produto */ }
  removeItem(productId: number): void { /* remove o produto do carrinho */ }
}
```

**Exemplo de frontend (Vue.js – Options API)**

```ts
export default defineComponent({
  components: { ProductCard },

  data() {
    const products: Product[] = [ /* lista de produtos */ ];
    const cart = new Cart();
    const cartItems: CartItem[] = [];

    return { products, cart, cartItems };
  },

  methods: {
    formatBRL(value: number): string { /* formata valor em R$ */ }
    syncCartItems(): void { /* sincroniza itens do carrinho */ }
    addToCart(product: Product): void { /* adiciona produto */ }
    increaseQuantity(productId: number): void { /* aumenta quantidade */ }
    decreaseQuantity(productId: number): void { /* diminui quantidade */ }
    removeItem(productId: number): void { /* remove produto */ }
  }
});
```

```vue
<template>
  <div class="app">
    ...
    <section class="app-products">
      <h2>Produtos</h2>
      <div class="product-grid">
        <ProductCard
          v-for="product in products"
          :key="product.id"
          :product="product"
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
          ....
        </div>
    </aside>
  </div>
</template>
```

# Como executar o projeto

**Clone o repositório:**

```bash
git clone https://github.com/skynetsites/vue-ecommerce-options-api.git
```

**Entre na pasta do projeto:**

```bash
cd vue-ecommerce-options-api
```

**Instale as dependências:**

```bash
npm install
```

**Execute o projeto (Backend):**

Na raiz do projeto:

```bash
npm run start:prod
```

**Execute o projeto (Frontend/Vue.js)**

Na pasta do frontend:

```bash
cd frontend
npm install
npm run dev
```

Abra no navegador o endereço indicado pelo Vite (geralmente `http://localhost:5173`).

**Para build de produção:**

```bash
cd frontend
npm run build
npm run preview
```

# Aprendizados

Durante o desenvolvimento desta atividade foi possível praticar:

- Tipagem forte utilizando TypeScript
- Criação de interfaces para modelar dados
- Uso de Enum para controle de permissões
- Aplicação de Programação Orientada a Objetos
- Manipulação de arrays com `.some()` e `.reduce()`
- Organização de projetos TypeScript + Vue.js

# Objetivo educacional

Projeto desenvolvido como atividade prática para aplicar:

- TypeScript (interfaces, enums, tipagem explícita).
- Programação Orientada a Objetos (encapsulamento, métodos).
- High Order Functions (`.some()`, `.reduce()`).
- Vue.js com Options API e integração com models e classes em TypeScript.

# Contribuição

Se quiser contribuir com feedback ou sugestões, fique à vontade para abrir uma **[Issue](https://github.com/skynetsites/vue-ecommerce-options-api/issues)** ou **[enviar ideias](https://github.com/skynetsites/vue-ecommerce-options-api/pulls)**. 

# Licença

Este projeto está licenciado sob a **Licença MIT**.

Veja o arquivo **[LICENSE](./LICENSE)** para mais detalhes.

# Autor

Projeto desenvolvido por **Isaias Oliveira**.  
Conecte-se comigo no **[in/skynetsites](https://www.linkedin.com/in/skynetsites/)**
