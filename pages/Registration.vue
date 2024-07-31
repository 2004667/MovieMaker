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
          <h1 class="mt-[5%]">Please first of all register</h1>
        </div>
        <div class="flex justify-center flex-col space-y-5 items-center mt-[-20%] max-[767px]:mt-[5%]">
          <div class="flex justify-center mt-[4%]">
            <input v-model="username" type="text" class="w-[250px] h-[40px] max-[767px]:w-[180px] max-[767px]:h-[30px] border-2 rounded-md pl-[10px]" placeholder="Login.." />
          </div>
          <div class="flex justify-center w-full">
            <input v-model="email" type="email" class="w-[250px] h-[40px] max-[767px]:w-[180px] max-[767px]:h-[30px] border-2 rounded-md pl-[10px]" placeholder="Email.." />
          </div>
          <div class="flex justify-center w-full">
            <input v-model="password" type="password" class="w-[250px] h-[40px] max-[767px]:w-[180px] max-[767px]:h-[30px] border-2 rounded-md pl-[10px]" placeholder="Password.." />
          </div>
          <div>
            <button @click="register" class="w-[200px] h-[40px] max-[767px]:h-[30px] max-[767px]:w-[130px] bg-[#2789C5] rounded-md text-[#FFFFFF]">Sign up</button>
          </div>
          <div class="flex space-x-1 items-center">
            <h1 class="text-[15px] max-[767px]:text-[10px]">If you have no account, please</h1>
            <NuxtLink to="/login">
              <h2 class="text-[15px] max-[767px]:text-[10px] text-[#2789C5] hover:text-[#8400FF]" id="signup"> log in </h2>
            </NuxtLink>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Registration',
  data() {
    return {
      username: '',
      email: '',
      password: ''
    };
  },
  methods: {
    validateEmail(email) {
      return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
    },
    validatePassword(password) {
      return /^(?=.*[a-zA-Z])(?=.*\d)[A-Za-z\d]{8,}$/.test(password);
    },
    register() {
      if (!this.username || !this.email || !this.password) {
        alert('All fields are required!');
        return;
      }

      if (!this.validateEmail(this.email)) {
        alert('Invalid email format!');
        return;
      }

      if (!this.validatePassword(this.password)) {
        alert('Password must be at least 8 characters long and contain both letters and numbers!');
        return;
      }

      const users = JSON.parse(localStorage.getItem('users')) || [];
      users.push({ username: this.username, email: this.email, password: this.password });
      localStorage.setItem('users', JSON.stringify(users));

      this.$router.push('/login');
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
