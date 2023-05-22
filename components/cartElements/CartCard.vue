<script setup>
const { updateItemQuantity, isUpdatingCart } = useCart();
const props = defineProps({
  item: { type: Object, required: true },
});
const productType = computed(() => (props.item.variation ? props.item.variation?.node : props.item.product?.node));
const quantity = ref(props.item.quantity);
const route = useRoute();
const router = useRouter();
let path = ref('')


function checkroute(goto) {
  if (route.path !== '/') {
    path = route.path.match(/^\/([^?\/]+)/)[1]
    if (path === 'product') {
      router.push({ path: `${goto}` });
    } else {
      router.push({ path: `product/${goto}` });
    }
  } else {
    path = route.path
    router.push({ path: `product/${goto}` });
  }
}

const updateQuantity = () => {
  updateItemQuantity(props.item.key, quantity.value);
};
</script>

<template>
  <li v-if="item" class="flex items-center gap-4">
    <!-- <NuxtLink @click="checkroute(props.item.product.node.slug)" :to="path === 'product' ? props.item.product.node.slug : `product/${props.item.product.node.slug}`"> -->
    <NuxtLink @click="checkroute(props.item.product.node.slug)">
      <img
        v-if="productType.image"
        width="64"
        height="64"
        class="w-16 h-16 rounded-lg"
        :src="productType.image.sourceUrl"
        :alt="productType.image.altText || productType.name"
        :title="productType.image.altText || productType.name"
        loading="lazy" />
    </NuxtLink>
    <div class="flex-1">
      <NuxtLink class="leading-tight" @click="checkroute(props.item.product.node.slug)">{{ productType.name }}</NuxtLink>
      <!-- <NuxtLink class="leading-tight" @click="checkroute(props.item.product.node.slug)" :to="path === 'product' ? props.item.product.node.slug : `product/${props.item.product.node.slug}`">{{ productType.name }}</NuxtLink> -->
      <ProductPrice class="mt-1 text-xs" :sale-price="productType.salePrice" :regular-price="productType.regularPrice" />
    </div>
    <input
      v-model.number="quantity"
      type="number"
      min="0"
      aria-label="Quantity"
      class="flex items-center justify-center w-16 gap-4 p-2 text-left bg-white border rounded-lg focus:outline-none"
      :disabled="isUpdatingCart"
      @input="updateQuantity" />
  </li>
</template>

<style scoped>
/* alwsys show up and down buttons on number inpout */
input[type='number']::-webkit-inner-spin-button,
input[type='number']::-webkit-outer-spin-button {
  opacity: 1;
}
</style>
