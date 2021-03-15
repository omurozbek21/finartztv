<template>
  <v-app>
    <div style="background-color: #f0f0f0">
      <v-toolbar dense>
        <v-toolbar-title
          style="font-size: 30px; color: #4527a0; font-weight: 700"
          >FINARTZ TV
          <img
            width="7%"
            :src="require(`@/assets/logo.png`)"
            alt="Dosya Logo"
          />
        </v-toolbar-title>
      </v-toolbar>
      <div class="row">
        <div class="col-md-3">
          <v-card class="my-12" max-width="374">
            <template slot="progress">
              <v-progress-linear
                color="deep-purple"
                height="10"
                indeterminate
              ></v-progress-linear>
            </template>

            <v-img
              height="300"
              :src="imgURL + this.moviedetail.poster_path"
            ></v-img>

            <v-card-title>{{ this.moviedetail.title }}</v-card-title>

            <v-card-text>
              <v-row align="center" class="mx-0" style="padding-bottom: 3%">
                <v-rating
                  :value="this.moviedetail.vote_average / 2"
                  color="amber"
                  dense
                  half-increments
                  readonly
                  size="14"
                ></v-rating>

                <div class="grey--text ml-4">
                  {{ this.moviedetail.vote_average / 2 }}
                </div>
              </v-row>
              <div>
                <v-card-title>Türler</v-card-title>
                <div
                  class="mb-2 mr-2 badge badge-warning"
                  v-for="i in moviedetail.genres"
                  :key="i.id"
                >
                  {{ i.name }}
                </div>
              </div>
              <v-divider class="mx-4"></v-divider>
              <v-card-title>Konu</v-card-title>
              <div>
                {{ moviedetail.overview }}
              </div>
            </v-card-text>
          </v-card>
        </div>
        <div class="col-md-9" style="padding-top: 3%; height: 50%">
          <h3 style="padding-left: 5%">Oyuncular</h3>
          <v-slide-group
            style="padding-bottom: 3%"
            class="pa4 movie_slider"
            next-icon="$next"
          >
            <v-slide-item v-for="i in actors" :key="i.id">
              <v-card :width="responsiveWidth" class="ma-2 trending_card">
                <img
                  class="item_poster"
                  height="230"
                  :width="responsiveWidth"
                  :src="imgURL + i.profile_path"
                />

                <v-card-subtitle class="show_title white--text">{{
                  i.name
                }}</v-card-subtitle>
                <p class="white--text release">
                  {{ i.character }}
                </p>
              </v-card>
            </v-slide-item>
          </v-slide-group>
          <div class="table-responsive">
            <table
              class="align-middle mb-0 table table-borderless table-striped table-hover"
            >
              <thead>
                <tr>
                  <th class="text-center">Kullanıcı Adı</th>
                  <th class="text-center">Rating</th>
                  <th class="text-center">Yorum</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="i in reviews" :key="i.id">
                  <td>
                    <div class="widget-content p-0">
                      <div class="widget-content-wrapper">
                        <div class="widget-content-left mr-3">
                          <div class="widget-content-left">
                            <img
                              width="40"
                              class="rounded-circle"
                              :src="imgURL + i.author_details.avatar_path"
                              alt
                            />
                          </div>
                        </div>
                        <div class="widget-content-left flex2">
                          <div class="widget-subheading opacity-7">
                            {{ i.author_details.username }}
                          </div>
                        </div>
                      </div>
                    </div>
                  </td>
                  <td class="text-center">
                    <v-rating
                      :value="(i.author_details.rating) / 2"
                      color="amber"
                      dense
                      half-increments
                      readonly
                      size="14"
                    ></v-rating>
                  </td>
                  <td class="text-center">{{ i.content }}</td>
                  <td class="text-center">{{ i["sip_user"] }}</td>
                </tr>
              </tbody>
            </table>
          </div>
          <!--p class="mt-3">Current Page: {{ currentPage }}</p-->
        </div>
      </div>
      <Footer />
    </div>
  </v-app>
</template>
<script>
import Footer from "../components/footer";
const axios = require("axios");
export default {
  components: {
    Footer,
  },
  data: () => ({
    page: 1,
    moviedetail: "",
    actors: [],
    reviews: [],
    imgURL: "https://image.tmdb.org/t/p/w342",
  }),
  methods: {
    getMoviedetail() {
      const movieId = this.$route.params.id;
      axios
        .get(
          "https://api.themoviedb.org/3/movie/" +
            movieId +
            "?api_key=b88d2c99815f98160d7e7d60aba9664f&language=tr"
        )
        .then((response) => {
          this.moviedetail = response.data;
        });
    },
    getMovieCredits() {
      const movieId = this.$route.params.id;
      axios
        .get(
          "https://api.themoviedb.org/3/movie/" +
            movieId +
            "/credits?api_key=b88d2c99815f98160d7e7d60aba9664f&language=tr"
        )
        .then((response) => {
          this.actors = response.data.cast;
        });
    },
    getReviews() {
      const movieId = this.$route.params.id;
      axios
        .get(
          "https://api.themoviedb.org/3/movie/" +
            movieId +
            "/reviews?api_key=b88d2c99815f98160d7e7d60aba9664f&language=en-US&page=1"
        )
        .then((response) => {
          this.reviews = response.data.results;
        });
    },
  },
  computed: {
    responsiveWidth() {
      switch (this.$vuetify.breakpoint.name) {
        case "xs":
          return 132;
        case "sm":
          return 140;
        case "md":
          return 145;
        case "lg":
          return 165;
        case "xl":
          return 165;
      }
    },
  },
  mounted() {
    this.getMoviedetail();
    this.getMovieCredits();
    this.getReviews();
  },
};
</script>
<style >
.trending_card {
  background: #0d47a1 !important;
  height: 350px;
}

.v-slide-group__next,
.v-slide-group__prev {
  min-width: 60px !important;
}

.v-btn--contained {
  box-shadow: none !important;
}

.show_title {
  font-size: 1rem;
  text-align: center;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.release {
  font-size: 1rem;
  text-align: center;
}

.v-progress-circular__info {
  font-size: 0.7rem;
}
</style>
