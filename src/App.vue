<template>
  <div>
    <Search @SearchRequested="search" />
    <transition name="fade">
      <div v-if="gifs.length > 0" class="container">
        <Gif v-for="gif in gifs" :gif="gif" :key="gif.id" />
      </div>
      <div class="loading" v-else>
        <h1 class="text">Loading...</h1>
      </div>
    </transition>
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
    trend() {
      this.getReq(
        `https://api.giphy.com/v1/gifs/trending?api_key=${process.env.VUE_APP_API_KEY}`,
      )
        .then((data) => {
          this.gifs = data;
        })
        .catch((err) => console.warn(err));
    },
    search(searchQuery) {
      this.searchQuery = searchQuery;
      if (!searchQuery) {
        this.trend();
      } else {
        this.gifs = [];
        this.getReq(
          `https://api.giphy.com/v1/gifs/search?api_key=${process.env.VUE_APP_API_KEY}&q=${searchQuery}`,
        )
          .then((data) => {
            this.gifs = data;
          })
          .catch((err) => console.warn(err));
      }
    },
  },
  watch: {
    gifs() {
      console.log(this.gifs);
    },
  },

  created() {
    this.trend();
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
  justify-content: space-evenly;
  margin-top: 10px;
  margin-bottom: 50px;
}

.container .image {
  margin: 5px;
}

.loading {
  margin-top: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.loading .text {
  color: #fff;
  background: #222;
  width: fit-content;
  padding: 10px 20px;
  border-radius: 10px;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
