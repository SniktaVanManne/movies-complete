<script>
import axios from 'axios'
export default {
  data() {
    return {
      query: '',
      results: '',
      movie: '',
      poster_path: 'https://image.tmdb.org/t/p/original/'
    }
  },
  methods: {
    getResults(query) {
      query = query.trim()

      axios
        .get(
          'https://api.themoviedb.org/3/search/movie?api_key=9cba81332618f150ad721b1be81a9d39&query=' +
            query +
            '&page=1&include_adult=false'
        )
        .then((response) => {
          this.results = response.data.results
        })
    },

    async clickRowHandler(movie) {
      const stringId = movie.id.toString()
      const fetchQuery =
        'https://api.themoviedb.org/3/movie/' +
        stringId +
        '?api_key=9cba81332618f150ad721b1be81a9d39'

      try {
        let response = await fetch(fetchQuery)
        this.movie = await response.json()
        this.poster_path = this.poster_path + this.movie.poster_path
      } catch (error) {
        console.log(error)
      }
      this.$emit('updateMovie', this.movie)
    }
  }
}
</script>

<template>
  <div class="greetings">
    <h1 class="green">Search Movies!</h1>
    <h3>
      <br />
      <!-- <input type="text" v-model="query" @blur="getResults(query)" /> -->
      <input type="text" v-model="query" />
      <br />
      <button @click="getResults(query)">Search Movies</button>
    </h3>
    <br />
    <div>
      <div>
        <table v-if="results" style="width: 100%">
          <tr>
            <th>Title</th>
            <th>Country</th>
            <th>Release Year</th>
          </tr>
          <tr v-for="movie in results" :key="movie.id" @click="clickRowHandler(movie)">
            <td>
              {{ movie.title }}
            </td>
            <td>
              {{ movie.original_language.toUpperCase() }}
            </td>
            <td>
              {{
                movie.release_date[0] +
                movie.release_date[1] +
                movie.release_date[2] +
                movie.release_date[3]
              }}
            </td>
          </tr>
          <tr></tr>
        </table>
      </div>
    </div>
  </div>
</template>

<style scoped>
table,
th,
td {
  padding: 1px;
  text-align: center;
  width: 100%;
  border: 1px solid whitesmoke;
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
