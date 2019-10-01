<template>
  <div class="row">
    <div class="columns" v-for="(post, index) in processedPosts" :key="index">
      <div class="card">
        <div class="card-divider">{{ post.title }}</div>
        <a :href="post.url" target="_blank"><img :src="post.image_url"></a>
        <div class="card-section">
          <p>{{ post.abstract }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'newsList',
  props: {
    results: {
      type: Array,
      required: false
    }
  },
  computed: {
    processedPosts () {
      let posts = this.results

      // Add image_url attribute
      posts.map(post => {
        let imgObj = post.multimedia.find(media => media.format === 'superJumbo')
        post.image_url = imgObj ? imgObj.url : 'https://placehold.it/320x230?text=N/A'
      })

      return posts
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.row {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  grid-template-rows: 1fr;
  column-gap: 16px;
  row-gap: 16px;
  padding: 0 16px;
}
.columns {
  border: 1px solid #e6e6e6;
}
a {
  display: block;
  text-align: center;
}
img {
  max-height: 100%;
  max-width: 100%;
}
.card-divider {
  background: #e6e6e6;
  padding: 12px;
}
.card-section {
  padding: 0 12px;
}
</style>
