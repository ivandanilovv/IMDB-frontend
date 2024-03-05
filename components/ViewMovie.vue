<template>
  <div class="row d-flex flex-row align-items-start justify-content-center mt-3">
    <div class="col col-11 col-lg-6 bg-white shadow m-2 p-4 rounded-4
      d-flex flex-column align-content-between justify-content-between">
      <div class="d-flex flex-row align-items-center justify-content-between">
        <div class="d-flex flex-row align-items-center justify-content-center">
          <i class="fa fa-lg fa-film" aria-hidden="true"></i>
          <NuxtLink :to="'/movie/' + movie.id" class="m-0 ms-2 fs-3 text-decoration-none text-black fw-bold">
            {{ movie.title }}
          </NuxtLink>
        </div>
        <p class="m-0 text-warning py-2 px-3 bg-light rounded-pill">{{ movie.genre }}</p>
      </div>
      <div class="my-2">
        <i class="fa fa-calendar" aria-hidden="true"></i><span class="m-0 ms-2">{{ movie.year }}</span>
      </div>
      <div class="mb-2 fs-5">
        {{ movie.description }}
      </div>
      <div class="d-flex flex-row align-items-center justify-content-between my-2">
        <div class="d-flex flex-row align-items-center justify-content-start">
          <i class="fa fa-star text-warning" aria-hidden="true"/>
          <div class="ms-2 d-flex flex-column align-items-start justify-content-center">
            <p class="m-0 fw-bold">
              {{ parseFloat(movie.averageRating).toFixed(1) }} <span class="fw-normal">/ 10</span>
            </p>
          </div>
        </div>
      </div>
      <div class="d-flex flex-row align-items-center justify-content-between my-2">
        <div class="fs-4 fw-bolder">
          <span class="fs-5"><i class="fa fa-pencil-square-o" aria-hidden="true"></i></span> User reviews
        </div>
        <NuxtLink id="leaveReview" :to="'/movies/' + movie.id + '/reviews/create'"
                  class="text-decoration-none text-warning p-2 rounded-2">
          <i class="fa fa-plus-circle" aria-hidden="true"></i> Leave your review
        </NuxtLink>
      </div>
      <div v-for="(review, i) in movie.reviews" class="fs-5 fst-italic">
        {{ i + 1 }}: {{ review.comment }}
      </div>
    </div>
  </div>
</template>

<script>
import CustomNavbar from "@/components/CustomNavbar";

export default {
  name: "ViewMovie",
  components: {CustomNavbar},
  props: {
    movie: Object,
  },
}
</script>

<style scoped>
.fw-bold {
  font-weight: 500 !important;
}

#leaveReview:hover {
  background-color: #fff3cd;
}
</style>
