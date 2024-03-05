<template>
  <main class="background-light pb-5">
    <custom-navbar :flag-home="flagHome" :flag-add="flagAdd"/>
    <div class="container">
      <form class="row d-flex flex-row align-items-start justify-content-center">
        <div class="col col-6 col-lg-3 mb-3">
          <label for="title" class="form-label">Title:</label>
          <input type="text" id="title" name="title" class="form-control rounded-pill"
                 placeholder="Search movies by name:"/>
        </div>
        <div class="col col-6 col-lg-3 mb-3">
          <label for="genre" class="form-label">Genre:</label>
          <select class="form-select rounded-pill" id="genre" name="genre">
            <option value="">Search movies by genre:</option>
            <option v-for="genre in uniqueGenres" :value="genre" class="">{{ genre }}</option>
          </select>
        </div>
        <div class="col col-6 col-lg-3 mb-3" :class="[flag ? 'd-none' : 'd-block']">
          <label for="year" class="form-label">Enter release year:</label>
          <input type="number" min="1900" :max="this.currentYear.getFullYear()" id="year" name="year"
                 v-model="exactYear" class="form-control rounded-pill"
                 placeholder="Search movies by release year:"/>
          <p class="m-0">
            You don't know the exact year?
            <span class="btn p-0 text-decoration-underline text-warning"
                  @click="flag = !flag"
                  :class="{'disabled disabled-link' : exactYear}">
              Click here!
            </span>
          </p>
        </div>
        <div class="col col-6 col-lg-3 mb-3" :class="[flag ? 'd-block' : 'd-none']">
          <label for="yearFrom" class="form-label">From year:</label>
          <input type="number" min="1900" :max="this.currentYear.getFullYear()" id="yearFrom" name="yearFrom"
                 class="form-control rounded-pill" placeholder="Search movies by release year:"/>
          <label for="yearTo" class="form-label">To year:</label>
          <input type="number" min="1900" :max="this.currentYear.getFullYear()" id="yearTo" name="yearTo"
                 class="form-control rounded-pill" placeholder="Search movies by release year:"/>
        </div>
        <div class="col col-6 col-lg-3 mt-4">
          <button type="submit" class="btn btn-warning text-white mt-2 mt-sm-0">
            <i class="fa fa-search" aria-hidden="true"></i> Search
          </button>
          <a href="/movies" class="btn btn-info text-white mt-2 mt-sm-0 mt-lg-2 mt-xl-0">
            <i class="fa fa-undo" aria-hidden="true"></i> Reset filters
          </a>
        </div>
      </form>
      <movie-card :movies="movies"/>
    </div>
  </main>
</template>

<style scoped>
.disabled-link {
  text-decoration: none !important;
  color: grey !important;
  border: 0;
}
</style>

<script>
import MovieCard from "@/components/MovieCard";
import CustomNavbar from "@/components/CustomNavbar";

export default {
  name: 'IndexPage',
  components: {MovieCard, CustomNavbar},
  data() {
    return {
      movies: [],
      currentYear: new Date(),
      exactYear: '',
      flag: false,
      flagHome: true,
      flagAdd: false,
    }
  },
  methods: {
    getMovies() {
      if (Object.keys(this.$route.query).length === 0)
        this.$axios.get('http://localhost:8080/movies')
          .then(response => (this.movies = response.data));
      else {
        let url = 'http://localhost:8080/movies';
        const title = this.$route.query.title || null;
        const genre = this.$route.query.genre || null;
        const year = this.$route.query.year || null;
        const yearFrom = this.$route.query.yearFrom || null;
        const yearTo = this.$route.query.yearTo || null;
        if (title)
          url += `${url.includes('?') ? '&' : '?'}title=${title}`;
        if (genre)
          url += `${url.includes('?') ? '&' : '?'}genre=${genre}`;
        if (year)
          url += `${url.includes('?') ? '&' : '?'}year=${year}`;
        if (yearFrom)
          url += `${url.includes('?') ? '&' : '?'}yearFrom=${yearFrom}`;
        if (yearTo)
          url += `${url.includes('?') ? '&' : '?'}yearTo=${yearTo}`;
        this.$axios.get(url)
          .then(response => (this.movies = response.data));
      }
    },
  },
  created() {
    this.getMovies();
  },
  computed: {
    uniqueGenres() {
      const uniqueGenres = new Set();
      this.movies.forEach(movie => {
        uniqueGenres.add(movie.genre);
      })
      return Array.from(uniqueGenres);
    },
    exactYear() {
      let exactYear = true;
      if (this.exactYear !== '')
        exactYear = false;
      return exactYear;
    }
  },
}
</script>
