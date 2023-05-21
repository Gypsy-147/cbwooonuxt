<script lang="ts" setup>
import { Splide, SplideSlide } from '@splidejs/vue-splide';
import '@splidejs/vue-splide/css';

</script>
<template>
    <div>
        <Splide :options="{ rewind: true, type: 'loop', perPage: 3, gap: 10, autoplay: true }" aria-label="My Favorite Images">
        <SplideSlide>
          <img src="/images/hero-3.jpg" alt="Sample 1" />
        </SplideSlide>
        <SplideSlide>
          <img src="/images/hero.jpeg" alt="Sample 2" />
        </SplideSlide>
      </Splide>
    </div>
</template>