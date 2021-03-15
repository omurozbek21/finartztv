<template>
  <div>
    <v-card flat height="200px" tile>
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
        <v-select
          style="padding-top: 1%"
          v-model="Selected"
          :items="CategoryItem"
          item-value="value"
          item-text="name"
          label="Kategori Filtresi"
          dense
          solo
        ></v-select>
        <v-btn icon>
          <v-icon>mdi-magnify</v-icon>
        </v-btn>
      </v-toolbar>
      <ul
        style="
          list-style-type: none;
          padding: 1%;
          overflow: hidden;
          background: whitesmoke;
          text-align: center;
          width: 100%;
          height: 50%;
          margin: auto;
        "
      >
        <li
          style="
            font-size: 20px;
            color: #4527a0;
            font-weight: 700;
            padding-right: 5%;
            text-align: center;
            display: inline-block;
            float: none;
          "
        >
          <strong>{{ total }}</strong
          ><br /><span>Listedeki Öğe</span>
        </li>

        <li
          style="
            font-size: 20px;
            color: #4527a0;
            font-weight: 700;
            padding-right: 5%;
            text-align: center;
            display: inline-block;
            float: none;
          "
        >
          <strong>{{ Math.round((totalrating / 10) * 100) }}%</strong
          ><br /><span>Ortalama Puan</span>
        </li>
      </ul>
    </v-card>
  </div>
</template>
<script>
export default {
  props: {
    total: {},
    totalrating: {},
  },
  data: () => ({
    Selected: null,
    CategoryItem: [
      {
        name: "Korku",
        value: "27",
      },
      {
        name: "Aksiyon",
        value: "28",
      },
      {
        name: "Romantik",
        value: "10749",
      },
          {
        name: "Bilim Kurgu",
        value: "878",
      },
      
    ],
  }),
  watch:{
    Selected:function(val){
      if(val != null){
        this.$emit('handleSelected',val)
      }
    }
  }
};
</script>

<style>
</style>



