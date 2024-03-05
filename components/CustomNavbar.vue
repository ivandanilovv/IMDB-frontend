<template>
  <div class="container ps-0 pt-3 mb-3">
    <nav class="navbar navbar-expand-lg">
      <div class="container d-flex flex-row justify-content-between align-items-center">
        <a href="/movies">
          <img src="../assets/images/imdb-logo.png" width="180" height="45" alt="Logo image"/>
        </a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse"
                data-bs-target="#navbar" aria-controls="navbar"
                aria-expanded="false"
                aria-label="Toggle navigation">
          <span class="navbar-toggler-icon bg-orange p-3 rounded-3"></span>
        </button>
        <div class="collapse navbar-collapse flex-column align-items-end justify-content-end" id="navbar">
          <ul class="navbar-nav text-center">
            <li class="nav-item">
              <a href="/movies" class="nav-link navbar-items-font ps-0 ps-lg-4 ps-xl-5 fs-4"
                 :class="{'fw-bold text-warning' : flagHome}">
                Home page
              </a>
            </li>
            <li class="nav-item">
              <a href="/movies/create" class="nav-link navbar-items-font ps-0 ps-lg-4 ps-xl-5 fs-4"
                 :class="{'fw-bold text-warning' : flagAdd}">
                Add new movie
              </a>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </div>
</template>

<script>
export default {
  name: "CustomNavbar",
  props: {
    flagAdd: Boolean,
    flagHome: Boolean,
  }
}
</script>

<style scoped>
</style>
