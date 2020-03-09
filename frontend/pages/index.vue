<template>
  <div>
    <div class="title">
      <h1>Welcome to My Radio Show</h1>
    </div>
    <div class="container">
      <div  v-for="album in filteredList" v-bind:key="album" class="max-w-sm rounded overflow-hidden shadow-lg p-1">
        <img
          class="w-full"
          :src="'http://localhost:1337' + album.image.url" alt="" width="300" height="300" 
        />
        <div class="px-6 py-4">
          <div class="font-bold text-xl mb-2">{{ album.name }}</div>
          <p
            class="text-gray-700 text-base"
          >{{ album.description }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import albumsQuery from "~/apollo/queries/album/albums";

export default {
  data() {
    return {
      albums: [],
      query: ""
    };
  },
  apollo: {
    albums: {
      prefetch: true,
      query: albumsQuery
    }
  },
  computed: {
    filteredList() {
      return this.albums.filter(album => {
        return album.name.toLowerCase().includes(this.query.toLowerCase());
      });
    }
  }
};
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
  @apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
.container {
  margin: 0 auto;
  min-height: 90vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  padding: top 1rem;
  text-align: center;
  font-size: 50px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
