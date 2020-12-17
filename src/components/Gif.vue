<template>
  <div class="image">
    <img :src="gif.images.fixed_height.url" alt="" />
  </div>
</template>

<script>
export default {
  props: ['gif'],
};
</script>

<style>
.image {
  width: auto;
  height: 100%;
  transition: 300ms all;
}
.image img {
  border-radius: 10px;
  width: 100%;
  box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.3);
}

.image:hover {
  transform: scale(1.3);
}
</style>
