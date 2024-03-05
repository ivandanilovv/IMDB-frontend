<template>
  <div class="row d-flex flex-row align-items-start justify-content-center mt-3">
    <div
      class="col col-11 col-lg-5 bg-white shadow m-2 p-4 rounded-4 zoom
      d-flex flex-column align-content-between justify-content-between"
      v-for="movie in movies">
      <div class="d-flex flex-row align-items-center justify-content-between">
        <div class="d-flex flex-row align-items-center justify-content-center">
          <i class="fa fa-lg fa-film" aria-hidden="true"></i>
          <NuxtLink :to="'/movie/' + movie.id" class="m-0 ms-2 fs-3 text-decoration-none text-black fw-bold">
            {{ movie.title }}
          </NuxtLink>
        </div>
        <p class="m-0 text-warning py-2 px-3 bg-light rounded-pill">{{ movie.genre }}</p>
      </div>
      <div>
        <i class="fa fa-calendar" aria-hidden="true"></i><span class="m-0 ms-2">{{movie.year}}</span>
      </div>
      <div class="d-flex flex-row align-items-center justify-content-between">
        <div class="d-flex flex-row align-items-center justify-content-start">
          <i class="fa fa-star fa-2x text-warning" aria-hidden="true"/>
          <div class="ms-2 d-flex flex-column align-items-start justify-content-center">
            <p class="m-0 fw-bold">
              {{ parseFloat(movie.averageRating).toFixed(1) }} <span class="fw-normal">/ 10</span>
            </p>
            <p class="m-0">
              From {{ movie.ratings.length }} users.
            </p>
          </div>
        </div>
        <NuxtLink :to="'/movie/' + movie.id" id="seeMore" class="text-decoration-none text-warning fs-3 px-3 py-2 rounded-5"
                  title="See more about this movie">
          &#x1F6C8;
        </NuxtLink>
      </div>
    </div>
    <div v-if="!movies.length">
      No movies found!
    </div>
  </div>
</template>

<script>
export default {
  name: "MovieCard",
  props: {
    movies: Array,
  }
}
</script>

<style scoped>
#seeMore:hover {
  cursor: pointer;
  background-color: #fff3cd;
}
.fw-bold {
  font-weight: 500 !important;
}
.zoom {
  transition: transform .2s;
}
.zoom:hover {
  transform: scale(1.05);
}
</style>
