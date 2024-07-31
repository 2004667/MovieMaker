<template>
  <div class="jj">
    <!-- Navigation -->
    <div class="bg-[#000000] w-full h-[60px] flex items-center px-4">
      <!-- Navigation Links -->
      <NuxtLink to="/home">
        <div class="ml-[15%]"><img src="/public/film-slate.png" alt="" width="50px"></div>
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
      <div class="max-[767px]:w-[150px] flex rounded-md   h-[30px]  bg-[#FFFFFF] max-[767px]:hidden" >
        <input type="text" placeholder="Search..." class="w-full h-full rounded-md pl-[10px]">
        <img src="/public/search.webp" alt="" class="h-[80%] mt-[1%]">
      </div>

      <!-- Logout Icon -->
      <div class="ml-4">
        <NuxtLink to="/login">
          <img src="/public/logout.png" alt="Logout" width="40px" class="max-[767px]:hidden">
        </NuxtLink>
      </div>
        <img src="/public/menubest.png" alt="" class="w-[35px] h-[35px] ml-[67%] md:hidden" @click="showdiv"> 
      </div>
      <div class="gh bg-[#FFFFFF] w-[full] h-[700px] flex-col md:hidden" v-if="gh">
        <div class="flex justify-center pt-[10%]">
         <div class="flex rounded-md w-[70%]  h-[40px]  bg-[#FFFFFF] border-[1px] " >
          <input type="text" placeholder="Search..." class="w-full h-full rounded-md pl-[10px]">
          <img src="/public/search.webp" alt="" class="h-[80%] mt-[1%]">
         </div>
        </div>
        <div class="flex justify-center mr-[30%]">
         <div class="flex-col justify-center  text-[21px] mt-[15%]">
          <NuxtLink to="/home">
          <div class="flex space-x-[10px]">
           <img src="/public/home-button.png" alt="" width="30px" height="20px">
           <h1 class="text-[#000000] font-[400]">Home</h1>
          </div>   
          </NuxtLink>
          <NuxtLink to="/mymovies">
          <div class="flex space-x-[10px] mt-[10%]">
            <img src="/public/video-camera.png" alt="" width="30px">
            <h1 class="text-[#000000] font-[400]">My movies</h1>
          </div>
          </NuxtLink>
          <NuxtLink to="/favorites">
          <div class="flex space-x-[10px] mt-[10%]">
            <img src="/public/star.png" alt="" width="30px">
           <h1 class="text-[#000000] font-[400]">Favorites</h1>
          </div>
          </NuxtLink>
          <NuxtLink to="/help">
          <div class="flex space-x-[10px] mt-[10%]">
            <img src="/public/help-desk.png" alt="" width="30px">
           <h1 class="text-[#000000] font-[400]">Help</h1>
          </div>
          </NuxtLink>
         </div>          
        </div>
        <div class="flex justify-center">
        <div class="w-[50%] h-[40px] bg-[#FFFFFF] border-[2px] rounded-md flex items-center mt-[15%]">
         <NuxtLink to="/login" class="flex items-center">
           <img src="/public/logout.png" alt="Logout" width="30px" class="md:hidden">
           <div class="flex justify-center">
            <h1 class="text-[22px] font-[400] md:hidden ml-[40px]">Exit</h1>
           </div>
         </NuxtLink>
        </div>
       </div>        
      </div>


    <!-- Main Content -->
    <div class="flex justify-center mt-[5%]">
      <div class="bg-[#CCCCCC] w-[90%] md:h-[1100px] max-[767px]:h-[auto] rounded-md flex-col border-[3px] border-[#000000]">
        <div class="justify-center flex">
         <div class="w-[90%] ">
          <div class="flex justify-center mt-[3%] "><h1 class="text-[30px] text-[#ffffff] font-[800]">MovieMaker App Instructions</h1></div>
          <div class="flex "><h1 class="text-[25px] text-[#ffffff] font-[800]">Overview:</h1></div>
          <div><h1 class="text-[18px] text-[#FFFFFF]">Welcome to the MovieMaker App! This app allows you to create and manage movies easily, from uploading movie details to marking favorites.</h1></div>
          <div class="flex mt-[3%]"><h1 class="text-[25px] text-[#ffffff] font-[800]">Creating a Movie:</h1></div>
          <div class="flex-col space-y-[3%]">
            <h1 class="text-[18px] text-[#FFFFFF]">1. Navigate to the Creation Page: Find the "Create Movie" section in the navigation menu.</h1>
            <h1 class="text-[18px] text-[#FFFFFF]">2. Upload a Photo: Click the upload button to add a movie poster image</h1>
            <h1 class="text-[18px] text-[#FFFFFF]">3. Enter Movie Details:</h1>
            <ul class="ml-[3%] flex-col space-y-3">
              <li class="text-[18px] text-[#FFFFFF]">Title: Enter the movie title.</li>
              <li class="text-[18px] text-[#FFFFFF]">Description: Provide a brief description of the movie.</li>
              <li class="text-[18px] text-[#FFFFFF]">Description: Provide a brief description of the movie.</li>
            </ul>
            <h1 class="text-[18px] text-[#FFFFFF]">4. Add Additional Information (Optional):</h1>
            <ul class="ml-[3%] flex-col space-y-3">
              <li class="text-[18px] text-[#FFFFFF]">Release Date: Enter the movie’s release date.</li>
            </ul>
          <div class="flex "><h1 class="text-[25px] text-[#ffffff] font-[800]">Managing Favorites:</h1></div>
          <div class="flex-col space-y-[1%]">
            <h1 class="text-[18px] text-[#FFFFFF]">1. Mark as Favorite: Click the star icon on a movie poster to add it to your favorites.</h1>
            <h1 class="text-[18px] text-[#FFFFFF]">2. View Favorites: Access the "Favorites" page from the navigation menu to see all your favorited movies.</h1>
            <h1 class="text-[18px] text-[#FFFFFF]">3. Remove from Favorites: Click the star icon again to unmark a movie.</h1>
          </div>
          <div class=""><h1 class="text-[18px] text-[#FFFFFF] mt-[50px]">If you still have trouble you can email to the techsupport:</h1></div>
          <div class=""><h1 class="text-[18px] text-[#FFFFFF] mt-[20px]">ilias2004nyssanbek@gmail.com</h1></div>
          </div>
         </div>
        </div>
      </div>
    </div>

    <!-- Pagination Controls -->
  </div>
</template>

<style scoped>
.jj {
  background-color: #6C6A6E;
}
</style>

<script>
export default {
  props: {
    movie: Object
  },
    data(){
    return{
      gh:false
    }
  },
  methods:{
     showdiv(){
      this.gh=!this.gh
     }
  }
}
</script>
