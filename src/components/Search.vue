<!--
<template lang="html">
<div class="">
  <v-form v-model="valid">
        <v-col cols="12" md="4">
          <v-text-field v-model="movie" :rules="nameRules" :counter="5" label="film name" required></v-text-field>
            <v-btn :disabled="!valid" color="success" class="mr-4" @click="validate">search</v-btn>
            <!-- why not green?? -->
        <!-- </v-col>
  </v-form>
  <div v-for="movie in movies" class="main-div">
    <Movie
      :popularity="movie.popularity"
      :overview="movie.overview"
      :title="movie.title"
      :voteAverage="movie.vote_average"
      :posterPath="movie.poster_path"
      />
  </div>
</div>
</template>


<script>
import axios from 'axios';
import Movie from './Movie.vue'
import Vuetify from 'vuetify'
export default {
  name: "SearchBar",
  components: {
    Movie
  },
  data: () => ({
    valid: true,
    movie: '',
    nameRules: [
      v => !!v || 'film name is required',
      v => v.length > 5 || 'film name must be not fewer than 5 characters',
    ],
    movies: [],
    movie: ""
  }),
  methods: {
    validate() {
      axios.get(`https://api.themoviedb.org/3/search/movie?api_key=d5554197c46a4661f13b298ecc0c4aad&query=${this.movie}`)
        .then(response => response.data.results.map(movie => {
          this.movies.push({
            popularity: movie.popularity,
            overview: movie.overview,
            title: movie.title,
            vote_average: movie.vote_average,
            posterPath: movie.poster_path
          })
        }))
      if (this.$refs.form.validate()) {
        this.snackbar = true
      }
    }
  }
}
</script>

<style lang="css" scoped>

</style> --> -->


<template lang="html">
<div class="">
  <v-form v-model="valid">
        <v-col cols="12" md="4">
          <v-text-field v-model="movie" :rules="nameRules" :counter="5" label="film name" required></v-text-field>
            <v-btn :disabled="!valid" color="success" class="mr-4" @click="validate">search</v-btn>
            <!-- why not green?? -->
        </v-col>
  </v-form>
  <div v-for="movie in movies" class="main-div">
    <Movie
      :popularity="movie.popularity"
      :overview="movie.overview"
      :title="movie.title"
      :voteAverage="movie.vote_average"
      :posterPath="movie.poster_path"
      />
  </div>
</div>
</template>


<script>
import axios from 'axios';
import Movie from './Movie.vue'
import Vuetify from 'vuetify'

export default {
  name: "SearchBar",
  components: {
    Movie
  },
  data: () => ({
    valid: true,
    movie: '',
    token: `d5554197c46a4661f13b298ecc0c4aad`,
    nameRules: [
      v => !!v || 'film name is required',
      v => v.length > 5 || 'film name must be not fewer than 5 characters',
    ],
    movies: [],
    movie: ""
  }),
  methods: {
    validate() {
      axios.get(this.searchUrl)
        .then(result => {
          this.movies = result.data.results;
        })
      if (this.$refs.form.validate()) {
        this.snackbar = true
      }
    }
  },
  computed: {
    searchUrl() {
      return `https://api.themoviedb.org/3/search/movie?api_key=${this.token}&query=${this.movie}`
    }
  }
}
</script>

<style lang="css" scoped>

</style>
