<script lang="ts" setup>
import { Splide, SplideSlide } from '@splidejs/vue-splide';
import '@splidejs/vue-splide/css';

</script>
<template>
    <div>
        <Splide :options="{ rewind: true, type: 'loop', perPage: 3, gap: 10, autoplay: true }" aria-label="My Favorite Images">
        <SplideSlide>
          <img src="/images/product1.png" alt="Product 1" />
        </SplideSlide>
        <SplideSlide>
          <img src="/images/product2.png" alt="Product 2" />
        </SplideSlide>
        <SplideSlide>
          <img src="/images/product3.png" alt="Product 3" />
        </SplideSlide>
      </Splide>
    </div>
</template>