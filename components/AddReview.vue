<template>
  <main>
    <custom-navbar/>
    <div class="m-5 p-5">
      <div class="row d-flex flex-row justify-content-evenly align-items-center">
        <div class="col-12 col-md-8 col-xl-6 bg-white rounded-5 mb-3 p-5">
          <div class="row">
            <div class="col-md-6">
              <div class="d-flex flex-column align-items-start justify-content-center h-100">
                <h5 class="fw-bolder fs-3 m-0">
                  <i class="fa fa-film" aria-hidden="true"></i>
                  {{ movie.title }}
                </h5>
                <p class="m-0 my-2">
                  <i class="fa fa-calendar" aria-hidden="true"></i>
                  {{ movie.year }}
                </p>
                <div class="d-flex flex-row align-items-center justify-content-start">
                  <i class="fa fa-star text-warning" aria-hidden="true"/>
                  <div class="ms-2 d-flex flex-column align-items-start justify-content-center">
                    <p class="m-0 fw-bold">
                      {{ parseFloat(movie.averageRating).toFixed(1) }} <span class="fw-normal">/ 10</span>
                    </p>
                  </div>
                </div>
              </div>
            </div>
            <div class="col-md-6 text-center">
              <form @submit.prevent="addReview">
                <label for="review" class="form-label fs-5 fst-italic">Add your review:</label>
                <textarea id="review" name="review" class="form-control" rows="3" v-model="review"
                          placeholder="Add your review here(optional)"/>
                <label for="rating" class="form-label fs-5 mt-2 fst-italic">Add rating 1-10</label>
                <input id="rating" type="number" min="1" max="10" name="rating" class="form-control" v-model="rating"
                       placeholder="Enter rating" required/>
                <button type="submit" class="btn btn-warning text-white mt-3 fw-bold">Submit</button>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import CustomNavbar from "@/components/CustomNavbar";

export default {
  name: "AddReview",
  components: {CustomNavbar},
  props: {
    movie: Object,
  },
  data() {
    return {
      review: '',
      rating: '',
    }
  },
  methods: {
    addReview() {
      const formData1 = new FormData();
      const formData2 = new FormData();
      formData1.append('review', this.review);
      formData2.append('rating', this.rating);
      if (this.review.length !== 0) {
        this.$axios.post('http://localhost:8080/movies/' + this.movie.id + '/review', formData1, {})
          .then((res) => {
            if (res.status === 200) {
              this.$axios.post('http://localhost:8080/movies/' + this.movie.id + '/rate', formData2, {})
                .then((res) => {
                  if (res.status === 200)
                    window.location.href = 'http://localhost:3000/movie/' + this.movie.id;
                })
            }
          })
      } else {
        this.$axios.post('http://localhost:8080/movies/' + this.movie.id + '/rate', formData2, {})
          .then((res) => {
            if (res.status === 200)
              window.location.href = 'http://localhost:3000/movie/' + this.movie.id;
          })
      }
    }
  }
}
</script>

<style scoped>
.fw-bolder {
  font-weight: 500 !important;
}
</style>
