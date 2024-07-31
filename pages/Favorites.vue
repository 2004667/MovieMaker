<template>
  <div class="jj">
    <!-- Navigation -->
    <div class="bg-[#000000] w-full h-[60px] flex items-center px-4">
      <!-- Navigation Links -->
      <NuxtLink to="/home">
        <div class="ml-[15%]">
          <img src="/public/film-slate.png" alt="Film Slate" width="50px">
        </div>
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
        <input type="text" placeholder="Search..." class="w-full h-full rounded-md pl-[10px]">
        <img src="/public/search.webp" alt="Search" class="h-[80%] mt-[1%]">
      </div>

      <!-- Logout Icon -->
      <div class="ml-4">
        <NuxtLink to="/login">
          <img src="/public/logout.png" alt="Logout" width="40px" class="max-[767px]:hidden">
        </NuxtLink>
      </div>
      <img src="/public/menubest.png" alt="Menu" class="w-[35px] h-[35px] ml-[67%] md:hidden" @click="toggleSidebar">
    </div>

    <!-- Sidebar -->
    <div class="gh bg-[#FFFFFF] w-[full] h-[700px] flex-col md:hidden" v-if="sidebarVisible">
      <div class="flex justify-center pt-[10%]">
        <div class="flex rounded-md w-[70%] h-[40px] bg-[#FFFFFF] border-[1px]">
          <input type="text" placeholder="Search..." class="w-full h-full rounded-md pl-[10px]">
          <img src="/public/search.webp" alt="Search" class="h-[80%] mt-[1%]">
        </div>
      </div>
      <div class="flex justify-center mr-[30%]">
        <div class="flex-col text-[21px] mt-[15%]">
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
          <NuxtLink to="/login" class="flex items-center w-full h-full">
            <img src="/public/logout.png" alt="Logout" width="30px" class="md:hidden">
            <h1 class="text-[22px] font-[400] ml-[10px]">Exit</h1>
          </NuxtLink>
        </div>
      </div>
    </div>

    <!-- Main Content -->
    <div class="flex justify-center mt-[5%]">
      <div class="bg-[#CCCCCC] w-[90%] h-[auto] md:pb-[10%] rounded-md flex-col border-[3px] border-[#000000]">
        <div class="ml-[6%] mt-[3%]">
          <h1 class="text-[30px] font-[700] text-[#000000]">Favorites</h1>
          <h2 class="text-[#000000]">Here are your favorite movies</h2>
        </div>
        <div class="flex flex-wrap justify-center mt-[3%]">
          <div v-if="favoriteMovies.length === 0" class="text-[#000000]">No favorite movies yet.</div>
          <div v-for="movie in favoriteMovies" :key="movie.id" class="bg-[#000000] w-[250px] h-[full] rounded-md text-[#FFFFFF] relative m-[10px]">
            <div class="w-full h-full bg-[#333] p-[10px] text-[#FFFFFF] text-center border-[10px] border-[#000000] rounded-[15px] hover:animate-pulse drop-shadow-lg">
              <img :src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`" alt="Poster" class="w-full h-[70%] object-cover rounded-md">
              <h3 class="mt-[3%] text-[#FFFFFF] text-[18px]">{{ movie.title }}</h3>
              <button @click="removeMovie(movie.id)" class="absolute top-[10px] right-[10px] bg-[#FF6347] text-[#FFFFFF] p-[5px] rounded-md">Remove</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      favoriteMovies: [],
      sidebarVisible: false,
    };
  },
  mounted() {
    this.loadFavorites();
  },
  methods: {
    loadFavorites() {
      const wishlist = localStorage.getItem('wishlist');
      this.favoriteMovies = wishlist ? JSON.parse(wishlist) : [];
    },
    removeMovie(movieId) {
      this.favoriteMovies = this.favoriteMovies.filter(movie => movie.id !== movieId);
      this.saveFavorites();
    },
    saveFavorites() {
      localStorage.setItem('wishlist', JSON.stringify(this.favoriteMovies));
    },
    toggleSidebar() {
      this.sidebarVisible = !this.sidebarVisible;
    }
  }
}
</script>

<style scoped>
.jj {
  background-color: #6C6A6E;
}
.poster-image {
  width: 100%;
  height: auto;
  border-radius: 10px;
}
</style>
