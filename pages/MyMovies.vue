<template>
  <div class="jj">

    <div class="bg-[#000000] w-full h-[60px] flex items-center px-4">

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

   
    <div class="flex justify-center mt-[5%]">
      <div class="bg-[#CCCCCC] w-[90%] h-[900px] rounded-md flex-col border-[3px] border-[#000000]">
        <div class="mt-[3%] ml-[8%]">
          <h1 class="text-[#FFFFFF] text-[30px] font-[700]">My movies</h1>
        </div>
        <div class="ml-[8%] mt-[1%]">
          <div class="bg-[#2789C5] w-[150px] h-[50px] rounded-md flex justify-center items-center hover:bg-[#141480]" @click="toggleForm">
            <h1 class="text-[20px] text-[#FFFFFF]">Create+</h1>
          </div>
        </div>
        <div class="flex justify-center mt-[3%]">
          <div class="bg-[#FFFFFF] w-[400px] h-[600px] rounded-md drop-shadow-lg flex-col justify-center" v-if="hector">
            <div class="bg-[#CCCCCC] w-[90%] h-[40%] rounded-md flex-col mt-[3%] ml-[5%]">
              <div class="flex justify-center items-center h-full">
                <img v-if="imagePreview" :src="imagePreview" alt="Image Preview" class="object-contain w-full h-full rounded-md" />
                <div v-else class="flex justify-center items-center w-full h-full">
                  <h1 class="text-[25px] font-[500] text-center" @click="triggerFileInput">Upload the image</h1>
                </div>
              </div>
            </div>
            <div class="flex-col justify-center space-y-[10px] mt-[5%]">
              <div class="flex justify-center">
                <input v-model="movieName" type="text" class="border-2 border-[#000000] w-[70%] h-[40px] rounded-md pl-[2%]" placeholder="Name of the movie:" />
              </div>
              <div class="flex justify-center">
                <input v-model="releaseDate" type="text" class="border-2 border-[#000000] w-[70%] h-[40px] rounded-md pl-[2%]" placeholder="Release date:" />
              </div>
              <div class="flex justify-center">
                <input v-model="score" type="text" class="border-2 border-[#000000] w-[70%] h-[40px] rounded-md pl-[2%]" placeholder="Score:" />
              </div>
              <div class="flex justify-center items-end">
                <textarea v-model="description" class="border-2 border-[#000000] w-[70%] h-[80px] rounded-md pl-[2%]" placeholder="Description:" />
              </div>
            </div>
            <div class="flex justify-center mt-[5%]">
              <input type="file" ref="fileInput" @change="handleFileUpload" class="hidden" />
              <button class="bg-[#2789C5] text-[#FFFFFF] w-[100px] h-[30px] rounded-md hover:bg-[#141480]" @click="submitForm">Submit</button>
            </div>
          </div>
        </div>
        
        <div class="flex flex-wrap justify-center mt-[5%] ml-[8%]">
          <div v-if="movies.length === 0" class="text-[#000000]">No movies added yet.</div>
          <div v-for="(movie, index) in movies" :key="index" class="bg-[#000000] w-[250px] h-[400px] rounded-md flex-col text-[#FFFFFF] relative m-[10px]">
            <div class="w-[250px] bg-[#333] p-[10px] text-[#FFFFFF] text-center border-[10px] border-[#000000] rounded-[15px] h-[400px] hover:animate-pulse drop-shadow-lg">
              <div>
                <img v-if="movie.image" :src="movie.image" alt="Movie Image" class="object-contain w-full h-full rounded-md" />
                <div v-else class="flex justify-center items-center h-full">
                  <h1 class="text-[20px] text-[#FFFFFF]">No Image</h1>
                </div>
              </div>
              <h3 class="mt-[3%] text-[#FFFFFF]">{{ movie.name }}</h3>
              <p><strong>Release Date:</strong> {{ movie.releaseDate }}</p>
              <p><strong>Score:</strong> {{ movie.score }}</p>
              <p><strong>Description:</strong> {{ movie.description }}</p>
              <button @click="removeMovie(index)" class="absolute top-[10px] right-[10px] bg-[#FF6347] text-[#FFFFFF] p-[5px] rounded-md">Remove</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.jj {
  background-color: #6C6A6E;
}

button {
  cursor: pointer;
}

img {
  object-fit: contain; 
}
</style>

<script>
export default {
  data() {
    return {
      hector: false, 
      movieName: '',
      releaseDate: '',
      score: '',
      description: '',
      file: null, 
      gh: false,
      imagePreview: '', 
      movies: [] 
    };
  },
  mounted() {
    this.loadMovies(); 
  },
  methods: {
    toggleForm() {
      this.hector = !this.hector; 
    },
    triggerFileInput() {
      this.$refs.fileInput.click(); 
    },
    handleFileUpload(event) {
      const file = event.target.files[0];
      if (file) {
        this.file = file;
        const reader = new FileReader();
        reader.onload = (e) => {
          this.imagePreview = e.target.result; 
        };
        reader.readAsDataURL(file); 
      }
    },
    showdiv() {
      this.gh = !this.gh;
    },
    async submitForm() {
      if (!this.file) {
        alert('Please select a file first.');
        return;
      }

      const formData = new FormData();
      formData.append('movieName', this.movieName);
      formData.append('releaseDate', this.releaseDate);
      formData.append('score', this.score);
      formData.append('description', this.description);
      formData.append('file', this.file);

      try {
        const response = await fetch('/upload', {
          method: 'POST',
          body: formData
        });
        const result = await response.json();
        alert('Upload successful!');

        this.movies.push({
          name: this.movieName,
          releaseDate: this.releaseDate,
          score: this.score,
          description: this.description,
          image: this.imagePreview
        });

        this.saveMovies(); 
        this.resetForm(); 
      } catch (error) {
        console.error('Error uploading file:', error);
        alert('Error uploading file.');
      }
    },
    resetForm() {
      this.movieName = '';
      this.releaseDate = '';
      this.score = '';
      this.description = '';
      this.file = null;
      this.imagePreview = ''; 
      this.hector = false;
    },
    removeMovie(index) {
      this.movies.splice(index, 1); 
      this.saveMovies(); 
    },
    saveMovies() {
      localStorage.setItem('movies', JSON.stringify(this.movies)); 
    },
    loadMovies() {
      const savedMovies = localStorage.getItem('movies');
      this.movies = savedMovies ? JSON.parse(savedMovies) : []; 
    }
  }
}
</script>