<template>
  <div class="home">
    <Hero />
    <div class="container movies">
      <div id="movie-grid" class="movie-grid">
        <div class="movie" v-for="(movie, index) in movies" :key="index">
          <div class="movie-img">
            <img
              :src="`https://image.tmdb.org/t/p/w300${movie.poster_path}`"
              alt="`${movie.original_title}`"
            />
          </div>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      movies: [],
    }
  },
  async fetch(){
    await this.getMovies()
  },
  methods: {
    async getMovies() {
      // TODO: install axios to make http requests
      const data = axios.get(
        process.env.BASE_URL + `movie/popular?api_key=${process.env.API_KEY}`
      )
      const result = await data
      result.data.results.forEach(movie => {
        this.movies.push(movie)
      })
      // console.log(this.movies);
    }
  }
}
</script>
<style>

.movie-grid{
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin-top: 40px;
}
.movie{
  margin-left: 10px;
  margin-right: 10px;
  margin-bottom: 30px;
  /* elevation */
  box-shadow: 0px 0px 10px rgba(0,0,0,0.5);
}
img{
  display: block;
}
</style>