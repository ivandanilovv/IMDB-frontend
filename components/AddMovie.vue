<template>
  <main class="background-light">
    <custom-navbar :flag-home="flagHome" :flag-add="flagAdd"/>
    <div class="container d-flex flex-column align-items-center justify-content-center">
      <form class="col col-11 col-lg-8 bg-white p-5 rounded-5 my-3" @submit.prevent="addMovie">
        <div class="mb-3">
          <label for="title" class="form-label fs-4">Movie title</label>
          <input type="text" class="form-control" id="title" v-model="movie.title"
                 placeholder="Enter movie title:" required>
        </div>
        <div class="mb-3">
          <label for="description" class="form-label fs-4">Movie description</label>
          <textarea rows="3" class="form-control" id="description" v-model="movie.description"
                    placeholder="Enter movie description" required/>
        </div>
        <div class="mb-3">
          <label for="genre" class="form-label fs-4">Movie genre</label>
          <input type="text" class="form-control" id="genre" v-model="movie.genre"
                 placeholder="Enter movie genre:" required>
        </div>
        <div class="mb-3">
          <label for="year" class="form-label fs-4">Release year:</label>
          <input type="number" min="1900" class="form-control" id="year" v-model="movie.year"
                 placeholder="Enter release year:" required>
        </div>
        <button type="submit" class="btn btn-warning text-white fw-bold">Submit</button>
        <div class="progress mt-3" style="height: 20px;">
          <div class="progress-bar progress-bar-striped bg-warning" role="progressbar"
               :style="{ width: progressBar + '%' }"
               aria-valuemin="0" aria-valuemax="100"></div>
        </div>
      </form>
    </div>
  </main>
</template>

<script>
import CustomNavbar from "@/components/CustomNavbar";

export default {
  name: "AddMovie",
  components: {CustomNavbar},
  data() {
    return {
      movies: [],
      movie: {
        title: '',
        description: '',
        genre: '',
        year: '',
      },
      currentYear: new Date(),
      flagHome: false,
      flagAdd: true,
    }
  },
  computed: {
    progressBar() {
      let progress = 0;
      for (let key in this.movie) {
        if (this.movie[key] !== '')
          progress += 25
      }
      return progress;
    }
  },
  methods: {
    addMovie() {
      const formData = new FormData();
      formData.append('title', this.movie.title);
      formData.append('description', this.movie.description);
      formData.append('genre', this.movie.genre);
      formData.append('year', this.movie.year);
      this.$axios.post('http://localhost:8080/movies', formData, {})
        .then((res) => {
          console.log(res.status);
          if (res.status === 200) {
            window.location.href = 'http://localhost:3000/movies'
          }
        })
    }
  }
}
</script>

<style scoped>

</style>
