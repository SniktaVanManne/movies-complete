<script>
export default {
  props: {
    //movieId: String,
    movie: Object,
    posterPath: String
  },
  data() {
    return {
      // movies: [],
    }
  },

  methods: {
    // async getData() {
    //   try {
    //     let response = await fetch(
    //       'https://api.themoviedb.org/3/movie/' +
    //         this.movieId +
    //         '?api_key=9cba81332618f150ad721b1be81a9d39'
    //     )
    //     this.movies = await response.json()
    //     this.poster_path = this.poster_path + this.movies.poster_path
    //   } catch (error) {
    //     console.log(error)
    //   }
    // }
  }

  //created() {
  //this.getData()
  //}
}
</script>

<template>
  <div v-if="movie">
    <!-- <ul v-for="movie in movies" :key="movie">
      <p>{{ movie }}</p>
    </ul> -->
    <h1 class="green">Title</h1>
    <ul>
      {{
        this.movie.title
      }}
    </ul>
    <br /><br />
    <ul v-if="this.movie.poster_path">
      <img height="380" width="250" v-bind:src="this.posterPath" />
    </ul>
    <br /><br />
    <h2 class="green">Summary</h2>
    <ul>
      {{
        this.movie.overview
      }}
    </ul>
    <h2 class="green" v-if="this.movie.genres.length > 0">Genres</h2>
    <ul v-if="this.movie.genres.length > 0" v-for="genre in this.movie.genres" :key="genre.id">
      {{
        genre.name
      }}
    </ul>
  </div>
</template>

<style scoped>
ul {
  font-weight: 400;
}

h1 {
  font-weight: 500;
  font-size: 2.6rem;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
