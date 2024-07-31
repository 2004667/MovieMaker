<template>
  <NuxtLink :to="`/cardtrailer/${movie.id}`">
    <div class="w-[250px] m-[15px] bg-[#333] p-[10px] text-[#FFFFFF] text-center border-[10px] border-[#000000] rounded-[15px] h-[400px] hover:animate-pulse drop-shadow-lg">
      <div>
        <img :src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`" alt="Poster" class="poster-image">
      </div>
      <h3 class="mt-[3%]">{{ movie.title }}</h3>

    </div>
  </NuxtLink>
</template>

<script>
export default {
  props: {
    movie: Object
  }
}
</script>

<style scoped>
.poster-image {
  width: 100%;
  height: 300px;
  border-radius: 2px;
}
</style>
