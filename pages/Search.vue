<template>
  <div class="flex rounded-md w-[70%] h-[40px] bg-[#FFFFFF] border-[1px]">
    <input v-model="searchQuery" type="text" placeholder="Search..." class="w-[85%] h-full pl-[10px]">
    <img src="/public/search.webp" alt="Search" @click="performSearch" class="cursor-pointer">
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: ''
    };
  },
  methods: {
    performSearch() {
      if (this.searchQuery.trim() === '') {
        alert('Please enter a search term.');
        return;
      }
      this.$router.push({ path: '/search', query: { query: this.searchQuery } });
    }
  }
}
</script>

<style scoped>
/* Add styles if needed */
</style>
