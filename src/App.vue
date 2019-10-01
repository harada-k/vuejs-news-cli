<template>
  <div id="app">
    <h1>VueNews</h1>
    <section class="search-area">
      <h2>Filter by Category</h2>
      <form>
        <div class="select-wrapper">
          <select v-model="section" @change="getPosts(section)">
            <option v-for="(section, index) in sections" :key="index" :value="section">{{ section }}</option>
          </select>
        </div>
      </form>
    </section>

    <section>
      <h2 v-if="!loading">{{ title }}</h2>
      <div v-if="loading" class="loader"><img src="http://cdnjs.cloudflare.com/ajax/libs/semantic-ui/0.16.1/images/loader-large.gif" alt="loader"></div>

      <news-list v-if="!loading" :results="results"></news-list>
    </section>
  </div>
</template>

<script>
import axios from 'axios'
import newsList from './components/news-list.vue'
import { config } from './config'

const NYTBaseUrl = 'https://api.nytimes.com/svc/topstories/v2/'
const ApiKey = config.KEY
const SECTIONS = 'home, arts, automobiles, books, business, fashion, food, health, insider, magazine, movies, national, nyregion, obituaries, opinion, politics, realestate, science, sports, sundayreview, technology, theater, tmagazine, travel, upshot, world' // From NYTimes

const buildUrl = (url) => {
  return `${NYTBaseUrl}${url}.json?api-key=${ApiKey}`
}

export default {
  name: 'app',
  components: {
    newsList
  },
  data () {
    return {
      results: [],
      sections: SECTIONS.split(', '), // create an array of the sections
      section: 'home', // set default section to 'home'
      loading: true,
      title: ''
    }
  },
  mounted () {
    this.getPosts(this.section)
  },
  methods: {
    getPosts (section) {
      this.loading = true
      let url = buildUrl(section)
      axios.get(url)
        .then((response) => {
          this.loading = false
          this.results = response.data.results
          let title = this.section !== 'home' ? `Top stories in ${this.section} today` : 'Top stories today'
          this.title = `${title} (${response.data.num_results})`
        })
        .catch((error) => {
          console.log(error)
        })
    }
  }
}
</script>

<style>
body {
  margin: 0;
}
#app {
  max-width: 1120px;
  margin: 0 auto 48px;
}
h1 {
  font-size: 20px;
  text-align: center;
}
h2 {
  font-size: 18px;
  font-weight: normal;
  margin: 0 0 16px 0;
  text-align: center;
}
.search-area {
  background: #eaeaea;
  margin: 0 16px 48px;
  min-width: 200px;
  padding: 16px;
}
select {
  appearance: none;
  background-color: #fefefe;
  border: 1px solid #cacaca;
  color: #0a0a0a;
  font-size: 16px;
  height: 32px;
  line-height: normal;
  padding: 4px 24px 4px 8px;
  width: 100%;
}
.select-wrapper {
  flex: 1 1 60%;
  margin: 0 0 12px;
  min-width: 60%;
  position: relative;
}
.select-wrapper:after {
  border-right: 1px solid #0a0a0a;
  border-top: 1px solid #0a0a0a;
  bottom: 0;
  content: '';
  display: block;
  height: 4px;
  margin: auto 0;
  position: absolute;
  right: 16px;
  top: 0;
  transform: rotate(135deg);
  width: 4px;
}
.loader {
  text-align: center;
}
</style>
