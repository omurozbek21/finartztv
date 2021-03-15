<template>
  <div>
    <div class="row" style="padding-left:3%;padding-bottom:3%">
      <v-card v-for="(item, i) in items.results" :key="i.id" :width="responsiveWidth" class="ma-2 trending_card" @click="routerpush(item.id)">
        <img
          class="item_poster"
          height="230"
          :width="responsiveWidth"
          :src="
            item.poster_path != null
              ? imgURL + item.poster_path
              : '../../assets/logo.png'
          "
          :alt="item.title ? item.title : item.name"
        />
        <v-row justify="center">
          <v-progress-circular
            :rotate="270"
            :size="37"
            :value="Math.round((item.vote_average / 10) * 100)"
            color="amber accent-4"
            >{{ Math.round((item.vote_average / 10) * 100) }}
            <v-icon color="amber accent-4" class="percent_sign" size="15"
              >mdi-percent</v-icon
            ></v-progress-circular
          >
        </v-row>

        <!--</v-img> -->
        <v-card-subtitle class="show_title white--text">{{
          item.title
        }}</v-card-subtitle>
        <p class="white--text release">
          {{
            item.release_date
              ? item.release_date
              : items.first_air_date 
          }}
        </p>
      </v-card>
    </div>
  </div>
</template>
<script>
const axios = require("axios");

export default {
  props: {
    items: {},
  },
  data() {
    return {
      imgURL: "https://image.tmdb.org/t/p/w342",
      model: null,
    };
  },
  methods: {
    routerpush(id){
       this.$router.push("/" + id);
    }
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
#ul_top_hypers li {
  display: inline;
}
</style>
