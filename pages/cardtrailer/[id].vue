<template>
  <div class="jj">
    <div class="bg-[#000000] w-full h-[60px] flex items-center px-4">
      <NuxtLink to="/home">
        <div class="ml-[15%]"><img src="/film-slate.png" alt="" width="50px"></div>
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
        <img src="/search.webp" alt="" class="h-[80%] mt-[1%]">
      </div>

      <div class="ml-4">
        <NuxtLink to="/login">
          <img src="/logout.png" alt="Logout" width="40px" class="max-[767px]:hidden">
        </NuxtLink>
      </div>
      <img src="/menubest.png" alt="Menu" class="w-[35px] h-[35px] ml-[67%] md:hidden" @click="toggleSidebar">
    </div>

    <div class="gh bg-[#FFFFFF] w-[full] h-[700px] flex-col md:hidden" v-if="sidebarVisible">
      <div class="flex justify-center pt-[10%]">
        <div class="flex rounded-md w-[70%] h-[40px] bg-[#FFFFFF] border-[1px] max-[767px]">
          <input type="text" placeholder="Search..." class="w-full h-full rounded-md pl-[10px]">
          <img src="/search.webp" alt="Search" class="h-[80%] mt-[1%]">
        </div>
      </div>
      <div class="flex justify-center mr-[30%]">
        <div class="flex-col text-[21px] mt-[15%]">
          <NuxtLink to="/home">
            <div class="flex space-x-[10px]">
              <img src="/home-button.png" alt="Home" width="30px" height="20px">
              <h1 class="text-[#000000] font-[400]">Home</h1>
            </div>
          </NuxtLink>
          <NuxtLink to="/mymovies">
            <div class="flex space-x-[10px] mt-[10%]">
              <img src="/video-camera.png" alt="My Movies" width="30px">
              <h1 class="text-[#000000] font-[400]">My movies</h1>
            </div>
          </NuxtLink>
          <NuxtLink to="/favorites">
            <div class="flex space-x-[10px] mt-[10%]">
              <img src="/star.png" alt="Favorites" width="30px">
              <h1 class="text-[#000000] font-[400]">Favorites</h1>
            </div>
          </NuxtLink>
          <NuxtLink to="/help">
            <div class="flex space-x-[10px] mt-[10%]">
              <img src="/help-desk.png" alt="Help" width="30px">
              <h1 class="text-[#000000] font-[400]">Help</h1>
            </div>
          </NuxtLink>
        </div>
      </div>
      <div class="flex justify-center">
        <div class="w-[50%] h-[40px] bg-[#FFFFFF] border-[2px] rounded-md flex items-center mt-[15%] hover:bg-[#2789C5] hover:text-[#FFFFFF]">
          <NuxtLink to="/login" class="flex items-center w-full h-full">
            <img src="/logout.png" alt="Logout" width="30px">
            <h1 class="text-[22px] font-[400] ml-[10px]">Exit</h1>
          </NuxtLink>
        </div>
      </div>
    </div>

    <div class="flex justify-center mt-[5%]">
      <div class="bg-[#000000] w-[90%] md:h-[700px] max-[767px]:h-auto rounded-md flex-col border-[3px] border-[#000000]">
        <div class="mt-[3%] ml-[11%]">
          <h1 class="text-[#FFFFFF] text-[30px] font-[700]">Movie Details</h1>
        </div>
        <div class="flex justify-center mt-[3%]">
          <div v-if="loading" class="text-[#FFFFFF]">Loading...</div>
          <div v-if="error" class="text-[#FF0000]">Error: {{ error }}</div>
          <div v-if="movieDetails" class="bg-[#000000] w-[80%] h-[auto] rounded-md drop-shadow-lg md:flex max-[767px]:flex-col space-x-[5%] p-4">
            <div class="flex justify-start">
              <iframe 
                v-if="trailerKey"
                :src="`https://www.youtube.com/embed/${trailerKey}`"
                frameborder="0"
                allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                allowfullscreen
                class="md:w-[560px] md:h-[315px] max-[767px]:w-[100%] trailer rounded-md"
              ></iframe>
              <p v-else class="text-[#FF0000]">No trailer available</p>
            </div>
            <div class="">
              <h2 class="text-[24px] font-bold text-[#FFFFFF]">{{ movieDetails.title }}</h2>
              <p class="text-[18px] text-[#FFFFFF]">{{ movieDetails.overview }}</p>
              <p class="text-[16px] text-[#FFFFFF]"><strong>Release Date:</strong> {{ movieDetails.release_date }}</p>
              <p class="text-[16px] text-[#FFFFFF]"><strong>Runtime:</strong> {{ movieDetails.runtime }} minutes</p>
              <p class="text-[16px] text-[#FFFFFF]"><strong>Genres:</strong> {{ movieDetails.genres.map(g => g.name).join(', ') }}</p>
              <p class="text-[16px] text-[#FFFFFF]"><strong>Vote Average:</strong> {{ movieDetails.vote_average }} / 10</p>
              <div class="md:flex max-[767px]:flex space-x-[3%] mt-[5%]">
                <div class="flex w-[150px] h-[40px] rounded-[100px] bg-[#2789C5] items-center hover:bg-[#1a41ba]">
                  <button class="text-[#FFFFFF] bg-[#2789C5] w-[100%] h-[40px] rounded-[100px] ml-[15%] hover:bg-[#1a41ba]">Trailer</button>
                  <img src="/trailer pro.png" alt="" class="w-[30px] h-[30px] mr-[5%]">
                </div>
                <div 
                  class="w-[50px] h-[40px] flex bg-[#2789C5] rounded-[100px] justify-center items-center hover:bg-[#1a41ba] cursor-pointer"
                  @click="toggleWishlist"
                >
                  <img :src="isInWishlist ? '/bookmark.png' : '/wishlist.png'" alt="Wishlist" class="w-[30px] h-[30px]">
                </div>              
              </div>
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
      movieDetails: null,
      trailerKey: null,
      loading: true,
      error: null,
      isInWishlist: false,
      sidebarVisible: false,
    };
  },
  async mounted() {
    const movieId = this.$route.params.id; 
    if (!movieId) {
      this.error = 'Movie ID is missing in the route parameters.';
      this.loading = false;
      return;
    }
    try {
      const response = await fetch(`https://api.themoviedb.org/3/movie/${movieId}?api_key=c6f06914c89e0d2d9127affd481b2189&language=en-US`);
      if (!response.ok) {
        throw new Error(`HTTP error! Status: ${response.status}`);
      }
      this.movieDetails = await response.json();

      const videoResponse = await fetch(`https://api.themoviedb.org/3/movie/${movieId}/videos?api_key=c6f06914c89e0d2d9127affd481b2189&language=en-US`);
      if (!videoResponse.ok) {
        throw new Error(`HTTP error! Status: ${videoResponse.status}`);
      }
      const videoData = await videoResponse.json();
      const trailer = videoData.results.find(video => video.type === 'Trailer');
      this.trailerKey = trailer ? trailer.key : null;

      this.checkWishlist();
    } catch (err) {
      this.error = err.message;
    } finally {
      this.loading = false;
    }
  },
  methods: {
    toggleWishlist() {
      const wishlist = this.getWishlist();
      const movieIndex = wishlist.findIndex(item => item.id === this.movieDetails.id);

      if (movieIndex === -1) {
        wishlist.push(this.movieDetails);
      } else {
        wishlist.splice(movieIndex, 1);
      }

      this.setWishlist(wishlist);
      this.checkWishlist();
    },
    getWishlist() {
      const wishlist = localStorage.getItem('wishlist');
      return wishlist ? JSON.parse(wishlist) : [];
    },
    setWishlist(wishlist) {
      localStorage.setItem('wishlist', JSON.stringify(wishlist));
    },
    checkWishlist() {
      const wishlist = this.getWishlist();
      this.isInWishlist = wishlist.some(item => item.id === this.movieDetails.id);
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
</style>
