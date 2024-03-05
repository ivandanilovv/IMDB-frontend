<template>
  <div class="background-light">
    <add-review :movie="movie"/>
  </div>
</template>

<script>
import AddReview from "@/components/AddReview";

export default {
  name: "create",
  components: {AddReview},
  data() {
    return {
      movie: {}
    }
  },
  methods: {
    getMovie() {
      this.$axios.get('http://localhost:8080/movie/' + this.$route.params.id)
        .then(res => (this.movie = res.data))
    }
  },
  created() {
    this.getMovie();
  }
}
</script>

<style scoped>

</style>
