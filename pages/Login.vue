<template>
  <div class="background">
    <NuxtRouteAnnouncer />
    <div class="header flex items-center justify-between w-full h-[80px] bg-[#000000] px-4">
      <img src="/film-slate.png" alt="Film Slate" class="md:w-[70px] md:pl-[20px] max-[767px]:w-[50px]" />
      <h1 class="text-[#FFFFFF] text-[24px] absolute inset-[3%] m-auto md:text-center max-[767px]:ml-[15%] items-center max-[767px]:text-[18px] max-[767px]:ml-[20%]">Welcome to the MovieMaker</h1>
    </div>
    <div class="flex justify-center md:mt-[5%] max-[767px]:mt-[20%]"> 
      <div class="bg-[#FFFFFF] md:w-[400px] md:h-[400px] max-[767px]:w-[300px]  max-[767px]:h-[300px] flex justify-center flex-wrap rounded-md drop-shadow-md space-x-[10px]">
        <div class="flex justify-center w-full">
          <h1 class="mt-[5%]">Please sign in</h1>
        </div>
        <div class="flex justify-center flex-col space-y-5 items-center mt-[-50%]">
          <input v-model="username" type="text" class="w-[250px] max-[767px]:w-[180px] max-[767px]:h-[30px] h-[40px] border-2 rounded-md pl-[10px]" placeholder="Login.." />
          <input v-model="password" type="password" class="w-[250px] max-[767px]:w-[180px] max-[767px]:h-[30px] h-[40px] border-2 rounded-md pl-[10px]" placeholder="Password.." />
          <button @click="login" class="md:w-[200px] max-[767px]:w-[130px] h-[40px] bg-[#2789C5] rounded-md text-[#FFFFFF] max-[767px]:h-[30px]">Sign in</button>
          <div class="flex space-x-1 items-center">
            <h1 class="text-[15px] max-[767px]:text-[10px]">If you have no account, please</h1>
            <NuxtLink to="/registration">
              <h2 class="text-[15px] max-[767px]:text-[10px] text-[#2789C5] hover:text-[#8400FF]" id="signup"> sign up</h2>
            </NuxtLink>
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
      username: '',
      password: ''
    };
  },
  methods: {
    login() {
      if (!this.username || !this.password) {
        alert('Please enter both username and password.');
        return;
      }

      const users = JSON.parse(localStorage.getItem('users')) || [];
      const user = users.find(u => u.username === this.username && u.password === this.password);

      if (user) {
        localStorage.setItem('loggedIn', 'true');
        console.log('Login successful. Redirecting to home page...');
        this.$router.push('/home');
      } else {
        alert('Invalid username or password.');
      }
    }
  }
}
</script>

<style scoped>
.background {
  background-image: url('/jeremy-yap-J39X2xX_8CQ-unsplash.jpg');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  height: 100vh; 
}
</style>
