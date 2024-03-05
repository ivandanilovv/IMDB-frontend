<template>
  <div class="background-light">
    <custom-navbar/>
    <div class="container">
      <view-movie :movie="movie"/>
    </div>
  </div>
</template>

<script>
import ViewMovie from "@/components/ViewMovie";
import CustomNavbar from "@/components/CustomNavbar";

export default {
  name: "_id",
  components: {CustomNavbar, ViewMovie},
  data() {
    return {
      movie: {}
    }
  },
  methods: {
    getMovie() {
      this.$axios.get('http://localhost:8080/movie/' + this.$route.params.id)
        .then(response => (this.movie = response.data));
    },
  },
  created() {
    this.getMovie();
  }
}
</script>

<style scoped>

</style>
