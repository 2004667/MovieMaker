<template>
  <div class="jj">
    <div class="bg-[#000000] w-full h-[60px] flex items-center px-4">
      <NuxtLink to="/home">
        <div class="ml-[15%]"><img src="/public/film-slate.png" alt="Film Slate" width="50px"></div>
      </NuxtLink>
      <div class="flex-1 flex justify-center space-x-[50px] pr-[30%] max-[767px]:hidden">
        <NuxtLink to="/home">
          <h1 class="text-[#FFFFFF]">Home</h1>
        </NuxtLink>
        <NuxtLink to="/mymovies">
          <h1 class="text-[#FFFFFF]">My movies</h1>
        </NuxtLink>
        <NuxtLink to="/favorites">
          <h1 class="text-[#FFFFFF]">Favorites</h1>
        </NuxtLink>
        <NuxtLink to="/help">
          <h1 class="text-[#FFFFFF]">Help</h1>
        </NuxtLink>
      </div>
      <div class="max-[767px]:w-[150px] flex rounded-md h-[30px] bg-[#FFFFFF] max-[767px]:hidden">
        <input v-model="searchQuery" @keyup.enter="performSearch" type="text" placeholder="Search..." class="w-full h-full rounded-md pl-[10px]">
        <img src="/public/search.webp" alt="Search" @click="performSearch" class="h-[80%] mt-[1%] cursor-pointer">
      </div>
      <div class="ml-4">
        <NuxtLink to="/login">
          <img src="/public/logout.png" alt="Logout" width="40px" class="max-[767px]:hidden">
        </NuxtLink>
      </div>
      <img src="/public/menubest.png" alt="Menu" class="w-[35px] h-[35px] ml-[67%] md:hidden" @click="showMenu"> 
    </div>

    <!-- Mobile Menu -->
    <div class="gh bg-[#FFFFFF] w-full h-[700px] flex-col md:hidden" v-if="menuVisible">
      <div class="flex justify-center pt-[10%]">
        <div class="flex rounded-md w-[70%] h-[40px] bg-[#FFFFFF] border-[1px]">
          <input v-model="searchQuery" @keyup.enter="performSearch" type="text" placeholder="Search..." class="w-full h-full rounded-md pl-[10px]">
          <img src="/public/search.webp" alt="Search" @click="performSearch" class="h-[80%] mt-[1%] cursor-pointer">
        </div>
      </div>
      <div class="flex justify-center mr-[30%]">
        <div class="flex-col justify-center text-[21px] mt-[15%]">
          <NuxtLink to="/home">
            <div class="flex space-x-[10px]">
              <img src="/public/home-button.png" alt="Home" width="30px" height="20px">
              <h1 class="text-[#000000] font-[400]">Home</h1>
            </div>
          </NuxtLink>
          <NuxtLink to="/mymovies">
            <div class="flex space-x-[10px] mt-[10%]">
              <img src="/public/video-camera.png" alt="My Movies" width="30px">
              <h1 class="text-[#000000] font-[400]">My movies</h1>
            </div>
          </NuxtLink>
          <NuxtLink to="/favorites">
            <div class="flex space-x-[10px] mt-[10%]">
              <img src="/public/star.png" alt="Favorites" width="30px">
              <h1 class="text-[#000000] font-[400]">Favorites</h1>
            </div>
          </NuxtLink>
          <NuxtLink to="/help">
            <div class="flex space-x-[10px] mt-[10%]">
              <img src="/public/help-desk.png" alt="Help" width="30px">
              <h1 class="text-[#000000] font-[400]">Help</h1>
            </div>
          </NuxtLink>
        </div>
      </div>
      <div class="flex justify-center">
        <div class="w-[50%] h-[40px] bg-[#FFFFFF] border-[2px] rounded-md flex items-center mt-[15%] hover:bg-[#2789C5] hover:text-[#FFFFFF]">
          <NuxtLink to="/login" class="flex items-center">
            <img src="/public/logout.png" alt="Logout" width="30px" class="md:hidden">
            <div class="flex justify-center">
              <h1 class="text-[22px] font-[400] md:hidden ml-[40px]">Exit</h1>
            </div>
          </NuxtLink>
        </div>
      </div>
    </div>

    <div class="flex justify-center">
      <div class="w-[600px] ml-[0%]">
        <h1 class="text-[50px] flex justify-center text-[#FFFFFF] font-[700]">MovieMaker</h1>
        <h2 class="text-[#FFFFFF] flex justify-center animate-pulse">MovieMaker - это платформа для опубликования собственного кино</h2>
      </div>
    </div>

    <div class="flex flex-wrap justify-center mt-[3%]">
      <MovieCard v-for="movie in movies" :key="movie.id" :movie="movie" />
    </div>

    <div class="flex justify-center mt-4 space-x-[50px]">
      <button @click="changePage(currentPage - 1)" :disabled="currentPage === 1" class="bg-gray-800 text-white px-4 py-2 rounded">Previous</button>
      <span class="flex items-center text-[22px] font-[600]">{{ currentPage }}</span>
      <button @click="changePage(currentPage + 1)" :disabled="currentPage >= totalPages" class="bg-gray-800 text-white px-4 py-2 rounded">Next</button>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import MovieCard from '@/pages/MovieCard.vue';
import { useRuntimeConfig } from '#app';

const config = useRuntimeConfig();
const apiKey = config.public.movieDbKey;

const movies = ref([]);
const currentPage = ref(1);
const totalPages = ref(1);
const menuVisible = ref(false);
const searchQuery = ref('');

async function fetchMovies(page = 1) {
  try {
    const response = await fetch(`https://api.themoviedb.org/3/movie/popular?api_key=${apiKey}&language=en-US&page=${page}`);
    
    if (!response.ok) {
      throw new Error('Network response was not ok.');
    }
    
    const data = await response.json();
    movies.value = data.results;
    totalPages.value = data.total_pages;
  } catch (error) {
    console.error('Error fetching data:', error);
  }
}

async function performSearch() {
  if (searchQuery.value.trim() === '') {
    alert('Please enter a search term.');
    return;
  }
  try {
    const response = await fetch(`https://api.themoviedb.org/3/search/movie?api_key=${apiKey}&language=en-US&query=${encodeURIComponent(searchQuery.value)}`);
    
    if (!response.ok) {
      throw new Error('Network response was not ok.');
    }
    
    const data = await response.json();
    movies.value = data.results;
    totalPages.value = 1; // Reset total pages for search results
  } catch (error) {
    console.error('Error fetching data:', error);
  }
}

function changePage(page) {
  if (page > 0 && page <= totalPages.value) {
    currentPage.value = page;
    localStorage.setItem('currentPage', page);
    fetchMovies(page);
  }
}

function showMenu() {
  menuVisible.value = !menuVisible.value;
}

onMounted(() => {
  currentPage.value = parseInt(localStorage.getItem('currentPage')) || 1;
  fetchMovies(currentPage.value);
});
</script>

<style scoped>
.jj {
  background-color: #6C6A6E;
}

button {
  cursor: pointer;
}
</style>
