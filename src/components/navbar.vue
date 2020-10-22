<template>
  <nav class="navbar navbar-light bg-light">
    <a class="navbar-brand">Giphy</a>
    <form class="form-inline">
      <input
        v-model="inputValue"
        class="form-control mr-sm-2"
        type="search"
        placeholder="Search"
        aria-label="Search"
      />
      <button
        @click="getItems"
        class="btn btn-outline-success my-2 my-sm-0"
        type="button"
      >
        Search
      </button>
    </form>
  </nav>
  <div class="container">
    <div v-for="(gif, i) in gifsAll" :key="i" class="row">
        <div class="card">
      <div class="card-body">{{gif.id}} <img :src="`${gif.images.original.url}.gif`"></div>
    </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      inputValue: "",
      gifsAll: []
    };
  },
  methods: {
    async getItems() {
      const API_KEY = "zQ7Td1uIaSn7fiZjfhIqNuVmXyvv2k8Q";
      const URL = `https://api.giphy.com/v1/gifs/search?q=${this.inputValue}&api_key=${API_KEY}`;
      const response = await fetch(URL);
      const data = await response.json();
      console.log(data);
      const gifs = data.data;
      console.log(gifs);
      return gifs.map(item => this.gifsAll.push(item))
    },
  },
};
</script>

<style>
.form-control {
  width: 500px;
}
.container{
    margin-top: 50px;
}
.col{
    margin-top: 50px;
}
</style>