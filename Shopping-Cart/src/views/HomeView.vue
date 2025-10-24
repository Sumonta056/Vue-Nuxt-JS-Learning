<script setup>
import { computed, ref, watch } from "vue";
const outOfStockImage =
  "https://t4.ftcdn.net/jpg/02/65/83/15/360_F_265831541_RUAcAGkikMs2WJOZ40D1BzjWqyp0MRze.jpg";
const productInfo = ref({
  productName: "Shoes",
  productDescription: "Here, You get topic quality shoe",
  productLink: "www.google.com",
  productImage: [
    {
      key: "Default",
      url: "https://images.unsplash.com/photo-1608231387042-66d1773070a5?ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&q=80&w=1074",
    },
    {
      key: "Green",
      url: "https://images.unsplash.com/photo-1512990414788-d97cb4a25db3?ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxzZWFyY2h8M3x8Z3JlZW4lMjBzaG9lc3xlbnwwfHwwfHx8MA%3D%3D&fm=jpg&q=60&w=3000",
    },
    {
      key: "Blue",
      url: "https://arthurknight.com/media/catalog/product/cache/8723b12f6326e9bdc6bc191d0c49a6b8/e/l/electric-blue-suede-mens-driving-shoes-1.jpg",
    },
  ],
  productInventory: [
    {
      key: "Default",
      stock: 15,
    },
    {
      key: "Green",
      stock: 100,
    },
    {
      key: "Blue",
      stock: 4,
    },
  ],
  price: [
    {
      key: "Default",
      amount: 2000,
    },
    {
      key: "Green",
      amount: 5000,
    },
    {
      key: "Blue",
      amount: 4000,
    },
  ],
  onSale: true,
  salesAmount: "50",
  salesOccasion: "Eid",
  sizes: ["L", "XL", "XXL"],
  details: [
    "Premium leather construction",
    "Cushioned memory foam insole",
    "Non-slip rubber outsole",
  ],
  variant: ["Default", "Green", "Blue"],
});

const selectedSize = ref(null);
const selectedVariant = ref("Default");
const currentImage = ref(productInfo.value.productImage[0].url);
const cartValue = ref(null);

const currentStock = computed(() => {
  const inventoryItem = productInfo.value.productInventory.find(
    (item) => item.key === selectedVariant.value
  );
  return inventoryItem ? inventoryItem.stock : 0;
});

const currentPrice = computed(() => {
  const inventoryItem = productInfo.value.price.find(
    (item) => item.key === selectedVariant.value
  );

  return inventoryItem ? inventoryItem.amount : 0;
});

const discountedPrice = computed(() => {
  const price = (currentPrice.value * productInfo.value.salesAmount) / 100;
  return currentPrice.value - price;
});

const onSaleMessage = computed(() => {
  return (
    productInfo.value.salesOccasion +
    " Sales " +
    productInfo.value.salesAmount +
    "%"
  );
});

const addToCart = () => {
  cartValue.value += 1;
  const inventoryItem = productInfo.value.productInventory.find(
    (item) => item.key === selectedVariant.value
  );
  inventoryItem.stock--;
};

// It can also be done using computed
watch(selectedVariant, (newVariant) => {
  const object = productInfo.value.productImage.find(
    (img) => img.key == newVariant
  );

  currentImage.value = object?.url || productInfo.value.productImage[0].url;
});
</script>

<template>
  <div
    class="min-h-screen bg-gradient-to-br from-slate-900 via-purple-900 to-slate-900"
  >
    <!-- Navbar -->
    <nav
      class="fixed top-0 left-0 right-0 z-50 bg-white/10 backdrop-blur-lg border-b border-white/20"
    >
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex items-center justify-between h-16">
          <!-- Logo/Brand -->
          <div class="flex items-center gap-2">
            <svg
              class="w-8 h-8 text-purple-400"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M16 11V7a4 4 0 00-8 0v4M5 9h14l1 12H4L5 9z"
              ></path>
            </svg>
            <span class="text-white text-xl font-bold">Vue Store</span>
          </div>

          <!-- Navigation Links -->
          <div class="hidden md:flex items-center gap-6">
            <a
              href="#"
              class="text-gray-300 hover:text-white transition-colors duration-200 text-sm font-medium"
              >Home</a
            >
            <a
              href="#"
              class="text-gray-300 hover:text-white transition-colors duration-200 text-sm font-medium"
              >Products</a
            >
            <a
              href="#"
              class="text-gray-300 hover:text-white transition-colors duration-200 text-sm font-medium"
              >About</a
            >
            <a
              href="#"
              class="text-gray-300 hover:text-white transition-colors duration-200 text-sm font-medium"
              >Contact</a
            >
          </div>

          <!-- Cart Button -->
          <div class="flex items-center gap-4">
            <button
              class="relative p-2 rounded-lg bg-white/10 hover:bg-white/20 transition-all duration-200 group"
            >
              <svg
                class="w-6 h-6 text-white"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M3 3h2l.4 2M7 13h10l4-8H5.4m0 0L7 13m0 0l-1.5 6M7 13l-1.5 6m1.5-6h10m0 0v6a2 2 0 01-2 2H9a2 2 0 01-2-2v-6m8 0V9a2 2 0 00-2-2H9a2 2 0 00-2 2v4.01"
                ></path>
              </svg>
              <span
                v-if="cartValue > 0"
                class="absolute -top-1 -right-1 w-5 h-5 bg-red-500 text-white text-xs font-bold rounded-full flex items-center justify-center animate-pulse"
              >
                {{ cartValue }}
              </span>
            </button>
          </div>
        </div>
      </div>
    </nav>

    <!-- Main Content -->
    <div class="flex justify-center items-center min-h-screen p-4 pt-24">
      <div
        class="max-w-sm w-full bg-white/10 backdrop-blur-lg rounded-2xl shadow-xl overflow-hidden border border-white/20"
      >
        <!-- Image Section -->
        <div class="relative h-56">
          <img
            class="h-full w-full object-cover"
            :src="currentImage"
            :alt="productInfo.productName"
          />
          <div class="absolute top-3 right-3">
            <span
              v-if="productInfo.onSale"
              class="px-2 py-1 bg-red-500 text-white text-xs font-bold rounded-full"
            >
              SALE
            </span>
            <span
              v-else
              class="px-2 py-1 bg-green-500 text-white text-xs font-bold rounded-full"
            >
              10% OFF
            </span>
          </div>

          <div class="absolute bottom-1 right-1" v-if="currentStock <= 0">
            <img :src="outOfStockImage" class="w-40 object-cover" />
          </div>
        </div>

        <!-- Content Section -->
        <div class="p-5">
          <!-- Title & Stock -->
          <div class="flex items-start justify-between mb-2">
            <h2 class="text-xl font-bold text-white flex gap-2">
              {{ productInfo.productName }}
              <p
                class="text-yellow-300 text-sm font-normal"
                v-if="productInfo.onSale == true"
              >
                {{ onSaleMessage }}
              </p>
            </h2>

            <div class="flex items-center gap-1">
              <div
                class="w-2 h-2 rounded-full"
                :class="{
                  'bg-green-400': currentStock >= 30,
                  'bg-yellow-400': currentStock >= 11 && currentStock <= 29,
                  'bg-red-400': currentStock < 11,
                }"
              ></div>
              <span class="text-gray-300 text-xs">
                {{ currentStock }} in stock
              </span>
            </div>
          </div>

          <!-- Description -->

          <p class="text-gray-300 text-sm mb-4">
            {{ productInfo.productDescription }}
          </p>

          <!-- Color Variants & Sizes Side by Side -->
          <div class="flex gap-4 mb-4">
            <!-- Color Variants -->
            <div class="flex-1">
              <label class="block text-gray-200 text-xs font-semibold mb-2"
                >Colors</label
              >
              <div class="flex gap-2">
                <button
                  v-for="variant in productInfo.variant"
                  :key="variant"
                  @click="selectedVariant = variant"
                  :class="[
                    'w-8 h-8 rounded-full transition-all duration-200',
                    selectedVariant === variant
                      ? 'ring-2 ring-white scale-110'
                      : 'hover:scale-105',
                    variant === 'Default' ? 'bg-gray-700' : '',
                    variant === 'Green' ? 'bg-green-600' : '',
                    variant === 'Blue' ? 'bg-blue-500' : '',
                  ]"
                  :title="variant"
                ></button>
              </div>
            </div>

            <!-- Sizes -->
            <div class="flex-1">
              <label class="block text-gray-200 text-xs font-semibold mb-2"
                >Sizes</label
              >
              <div class="flex gap-2">
                <button
                  v-for="size in productInfo.sizes"
                  :key="size"
                  @click="selectedSize = size"
                  :class="[
                    'px-3 py-1 text-sm font-semibold rounded-lg transition-all duration-200',
                    selectedSize === size
                      ? 'bg-purple-600 text-white'
                      : 'bg-white/10 text-gray-300 hover:bg-white/20',
                  ]"
                >
                  {{ size }}
                </button>
              </div>
            </div>
          </div>

          <!-- Product Details -->
          <div class="mb-4">
            <label class="block text-gray-200 text-xs font-semibold mb-2"
              >Product Details</label
            >
            <ul class="space-y-1">
              <li
                v-for="(detail, index) in productInfo.details"
                :key="index"
                class="text-gray-300 text-xs flex items-center gap-2"
              >
                <span class="w-1 h-1 bg-purple-400 rounded-full"></span>
                {{ detail }}
              </li>
            </ul>
          </div>

          <div class="text-gray-300 text-xs mb-4 flex gap-1">
            <div :class="[productInfo.onSale ? 'line-through' : '']">
              <span class="font-semibold">Price :</span>
              {{ currentPrice }} BDT
            </div>
            <span v-if="productInfo.onSale" class="text-yellow-300">
              Discounted Price {{ discountedPrice }} BDT</span
            >
          </div>

          <!-- Shop Now Button -->
          <div class="flex gap-2">
            <a
              :href="productInfo.productLink"
              class="flex-1 inline-flex items-center justify-center gap-2 px-4 py-2.5 bg-gradient-to-r from-blue-600 to-purple-600 text-white font-semibold rounded-xl shadow-lg hover:shadow-xl transition-all duration-300 transform hover:scale-105"
            >
              <span>Shop Now</span>
              <svg
                class="w-4 h-4"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M13 7l5 5m0 0l-5 5m5-5H6"
                ></path>
              </svg>
            </a>
            <button
              :class="[
                'flex-1 inline-flex items-center justify-center gap-2 px-4 py-2.5   font-semibold rounded-xl shadow-lg hover:shadow-xl transition-all duration-300 transform hover:scale-105',
                currentStock <= 0
                  ? 'bg-red-700 text-white cursor-not-allowed'
                  : 'bg-gradient-to-r from-gray-300 to-stone-200 text-black cursor-pointer',
              ]"
              v-on:click="addToCart"
              :disabled="currentStock <= 0"
            >
              <svg
                class="w-4 h-4"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M3 3h2l.4 2M7 13h10l4-8H5.4m0 0L7 13m0 0l-1.5 6M7 13l-1.5 6m1.5-6h10m0 0v6a2 2 0 01-2 2H9a2 2 0 01-2-2v-6m8 0V9a2 2 0 00-2-2H9a2 2 0 00-2 2v4.01"
                ></path>
              </svg>
              <span v-if="currentStock > 0"> Add to Cart</span>
              <span v-else>Out of Stock</span>
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
