<template>
  <v-app>
    <div>
        <Header 
      :total="items.total_results"
      :totalrating="items.average_rating"
      @handleSelected="type=$event"
      />
        <FilmList :items="items" />
      <div class="text-center">
        <v-pagination
          v-model="page"
          :length="totalpage"
          circle
        ></v-pagination>
      </div>
      <Footer />
    </div>
  </v-app>
</template>

<script>
import Header from "../components/appheader";
import FilmList from "../components/filmlist";
import Footer from "../components/footer";
const axios = require("axios");
export default {
  components: {
    Header,
    FilmList,
    Footer,
  },
  data: () => ({
    items: [],
    page: 1,
    totalpage: 0,
    type:null
  }),
  methods: {
    getData(page,type) {
      this.items=[];
      this.totalpage=0;
      var url ;
      if(type==null){
        url="https://api.themoviedb.org/4/list/7081954?page=" +page +"&api_key=b88d2c99815f98160d7e7d60aba9664f&language=tr-TR"
      }
      else{
       url="https://api.themoviedb.org/4/list/7081954?page=" +page +"&api_key=b88d2c99815f98160d7e7d60aba9664f&language=tr-TR&with_genres="+type
      }
      axios
        .get(
         url
        )
        .then((response) => {
          this.totalpage = response.data.total_pages;
          this.items = response.data;
        });
    },

  },
  mounted() {
    this.getData();
  },
  watch:{
    page:function(newVal,oldVal){
       if(newVal != oldVal){
        this.getData(newVal,this.type)
       }
    },
      type:function(newVal,oldVal){
       if(newVal != oldVal){
        this.getData(this.page,newVal)
       }
    }
  }
};
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
