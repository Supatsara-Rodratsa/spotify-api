<script setup>
import {ref, onErrorCaptured} from 'vue';
import Spotify from './components/Spotify.vue';
import LazyLoadCard from './components/LazyLoadCard.vue';
import AlbumDetail from './components/AlbumDetail.vue';
import Error from './components/Error.vue'
const error = ref('');

onErrorCaptured((err) => {
    error.value = err
    return true
});

</script>

<template>
  <h1 class="flex topic">New Release Album</h1>
  <Suspense>
    <Spotify/>
    <template #fallback>
      <div class="flex-row" v-if="!error">
        <div v-for="item in 5" v-bind:key="item">
          <LazyLoadCard/>
         </div>
      </div>
      <Error :error="error" v-else/>
    </template>
  </Suspense>
</template>

<style scoped>

</style>
