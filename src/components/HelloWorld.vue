<template>
  <div class="hello">
    <h2>{{ name }}</h2>
    <div class="d-flex flex-wrap" id="movieContainer">
      <!-- <div class="flex-fill"> -->
        <b-card
          v-for="(movie, index) in movies"
          :key="index"
          v-bind:title="movie.title"
          v-bind:img-src="
            'https://image.tmdb.org/t/p/w200/' + movie.poster_path
          "
          img-alt="Image"
          img-top
          tag="article"
          style="max-width: 20rem;"
          class="mb-2"
        >
          <!-- {{movie}} -->
          <MovieCard :movie-prop="movie"></MovieCard>
        </b-card>
      </div>
    <!-- </div> -->
  </div>
</template>

<script>
import MovieCard from "./MovieCard.vue";
export default {
  components: { MovieCard },
  name: "HelloWorld",
  data() {
    return {
      name: "Martin's Movies",
      query: null,
      movies: []
    };
  },
  methods: {
    fetchMovies() {
      //fetch(`https://jsonplaceholder.typicode.com/posts?search=${this.query}`)

      //let promise = fetch('https://jsonplaceholder.typicode.com/posts?search')
      const API_KEY = "1e448e0dfcdbb565f5d329820065b4d2";
      var searchQuery = this.query;

      let promise = fetch(
        "https://api.themoviedb.org/3/movie/popular?api_key=" +
          API_KEY +
          "&language=en-US&page=1"
      );

      console.log(
        "https://api.themoviedb.org/3/movie/popular?api_key=" +
          API_KEY +
          "&language=en-US&page=1"
      );
      let jsonPromise = promise.then(function(response) {
        return response.json();
      });

      jsonPromise.then(jsonData => {
        console.log(jsonData);
        this.movies = jsonData.results;
      });
    }
  },
  mounted() {
    this.fetchMovies();
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

<style scoped>
#movieContainer{
margin:3em 3em 3em 6em;
}



h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
