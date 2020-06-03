<template>
  <div class="container">
    <nuxt-link to="/">Regresar</nuxt-link>
    <h1 class="title">{{ album.title }}</h1>
    <div class="columns is-multiline">
      <div class="column is-one-quarter" v-for="photo in photos" :key="photo.id">
        <img :src="photo.url" :alt="photo.title">
      </div>
    </div>
  </div>
</template>

<script>
import router from 'vue-router';
import env from '../../config/env';
import axios from 'axios';

export default {
  name: 'AlbumIndvPage',
  data() {
    return {
      album: {},
      photos: []
    }
  },
  created: async function() {
    let albumId = this.$route.params.id;
    let albumData = await axios.get(`${env.endpoint}/albums/${albumId}`);
    this.album = albumData.data;
    let photosData = await axios.get(`${env.endpoint}/albums/${albumId}/photos`);
    this.photos = photosData.data;
  }
};
</script>

<style scoped>
.container {
  text-align: center;
}
.title {
  margin-top: 100px;
}
</style>
