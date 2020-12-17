<template>
  <div>
    <Search @SearchRequested="search" />
    <div class="container">
      <Gif v-for="gif in gifs" :gif="gif" :key="gif.id" />
    </div>
  </div>
</template>

<script>
import Gif from '@/components/Gif';
import Search from '@/components/Search';
import Axios from 'axios';
export default {
  components: {
    Gif,
    Search,
  },
  data() {
    return {
      gifs: [],
    };
  },
  methods: {
    async getReq(url) {
      if (!url) return;
      const res = await Axios.get(url);
      const data = await res.data.data;
      return data;
    },
    search(searchQuery) {
      this.searchQuery = searchQuery;
      if (!searchQuery) return;
      this.gifs = [];
      this.getReq(
        `https://api.giphy.com/v1/gifs/search?api_key=${process.env.VUE_APP_API_KEY}&q=${searchQuery}`,
      )
        .then((data) => {
          this.gifs = data;
        })
        .catch((err) => console.warn(err));
    },
  },
  watch: {
    gifs() {
      console.log(this.gifs);
    },
  },

  created() {
    this.getReq(
      `https://api.giphy.com/v1/gifs/trending?api_key=${process.env.VUE_APP_API_KEY}`,
    )
      .then((data) => {
        this.gifs = data;
      })
      .catch((err) => console.warn(err));
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin-top: 10px;
  margin-bottom: 50px;
}

.container .image {
  margin: 5px;
}
</style>
