<template>
  <div class="container">
    <div class="row p-5">
      <h1 class="text-center mb-5 fw-light">Search for Your Movies</h1>
      <form class="row g-2" @submit.prevent="searchMovies">
        <div class="col-sm-9">
          <input
            class="form-control"
            type="text"
            placeholder="Example: The Matrix"
            aria-label="Search"
            v-model="query"
            required
          />
        </div>
        <div class="col-sm-2">
          <input
            type="number"
            class="form-control"
            placeholder="Year (optional)"
            v-model="filteredYear"
          />
        </div>
        <div class="col-sm-1">
          <button class="btn btn-primary w-100 fw-bold" type="submit">
            Search
          </button>
        </div>
      </form>
    </div>
    <div class="row" v-if="errMsg">
      <div class="alert alert-danger" role="alert">
        {{ errMsg }}
      </div>
    </div>
  </div>

  <div class="container">
    <div class="row">
      <div
        class="col-sm-3 text-white mt-3"
        v-for="movie in movies"
        :key="movie.imdbID"
      >
        <div
          class="card"
          data-bs-toggle="modal"
          data-bs-target="#staticBackdrop"
        >
          <img
            class="card-img-top"
            :src="
              movie.Poster !== 'N/A'
                ? movie.Poster
                : 'https://placehold.co/300x445?text=No+Poster'
            "
            alt="Movie Poster"
            style="height: 445px; object-fit: cover"
          />
          <div class="card-body" style="color: #8faac7">
            <h5 class="card-title text-truncate">{{ movie.Title }}</h5>
            <p class="card-text">{{ movie.Year }}</p>
          </div>
        </div>
        <form
          class="modal fade"
          id="staticBackdrop"
          data-bs-backdrop="static"
          data-bs-keyboard="false"
          tabindex="-1"
          aria-labelledby="staticBackdropLabel"
          aria-hidden="true"
          novalidate
          @submit.prevent
        >
          <div class="modal-dialog modal-dialog-centered">
            <div class="modal-content">
              <div class="modal-header">
                <h2 class="modal-title fs-5" id="staticBackdropLabel">
                  Ratings
                </h2>
                <button
                  type="button"
                  class="btn-close"
                  data-bs-dismiss="modal"
                  aria-label="Close"
                ></button>
              </div>
              <div class="modal-body">
                <div class="form-check form-check-inline">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="inlineRadioOptions"
                    id="inlineRadio1"
                    value="option1"
                  />
                  <label class="form-check-label" for="inlineRadio1">1</label>
                </div>
                <div class="form-check form-check-inline">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="inlineRadioOptions"
                    id="inlineRadio2"
                    value="option2"
                  />
                  <label class="form-check-label" for="inlineRadio2">2</label>
                </div>
                <div class="form-check form-check-inline">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="inlineRadioOptions"
                    id="inlineRadio3"
                    value="option3"
                  />
                  <label class="form-check-label" for="inlineRadio3">3</label>
                </div>
                <div class="form-check form-check-inline">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="inlineRadioOptions"
                    id="inlineRadio4"
                    value="option4"
                  />
                  <label class="form-check-label" for="inlineRadio4">4</label>
                </div>
                <div class="form-check form-check-inline">
                  <input
                    class="form-check-input"
                    type="radio"
                    name="inlineRadioOptions"
                    id="inlineRadio5"
                    value="option5"
                  />
                  <label class="form-check-label" for="inlineRadio5">5</label>
                </div>
                <div class="mt-3">
                  <label for="ratingComment" class="form-label">Comment</label>
                  <textarea
                    class="form-control"
                    id="ratingComment"
                    rows="3"
                  ></textarea>
                </div>
              </div>
              <div class="modal-footer">
                <button
                  type="submit"
                  class="btn btn-primary"
                  data-bs-dismiss="modal"
                >
                  Save
                </button>
              </div>
            </div>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<style scoped>
h1 {
  color: #a6b7c9;
}
div.card {
  background-color: #445566;
}
</style>

<script>
export default {
  name: "HomeView",
  data() {
    return {
      query: "",
      movies: [],
      filteredYear: "",
      errMsg: "",
    };
  },
  methods: {
    async searchMovies() {
      const apiKey = "2d865e56";
      let url = `https://www.omdbapi.com/?apikey=${apiKey}&s=${encodeURIComponent(
        this.query
      )}`;
      if (this.filteredYear) {
        url += `&y=${this.filteredYear}`;
      }
      this.movies = [];

      const res = await fetch(url);
      try {
        const data = await res.json();
        if (data.Response == "True") {
          this.errMsg = "";
          this.movies = data.Search;
        } else {
          this.errMsg = data.Error;
          this.movies = [];
        }
      } catch (error) {
        console.error("Error fetching movies:", error);
        this.movies = [];
      }
    },
  },
  mounted() {
    if (this.$root.authenticated == false) {
      this.$router.replace({ name: "login" });
    }
  },
};
</script>
