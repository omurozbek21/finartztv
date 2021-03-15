<template>
  <v-footer color="blue darken-4" padless>
    <v-col class="text-center footer_items" cols="12">
      <v-card-text>
          <img
              width="7%"
              :src="require(`@/assets/logo.png`)"
              alt="Dosya Logo"
            />
      </v-card-text>
      {{ new Date().getFullYear() }} — <strong>&#169; Ömür Özbek</strong>
      <v-card-text id="text"
        >The site is designed and built by me. Data used is provided by
        <a href="https://www.themoviedb.org/">TMDB</a></v-card-text
      >
    </v-col>
  </v-footer>
</template>

<script>
export default {
  data: () => ({

  }),
}
</script>

<style>
.footer_items {
  color: white;
}

#footer_icon {
  color: white !important;
}

#text {
  color: white;
  text-align: center;
}
</style>