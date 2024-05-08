<script>
import { store } from "../src/store";
import axios from "axios";
import AppHeader from "./components/AppHeader.vue";
import AppMain from "./components/AppMain.vue";
import AppFooter from "./components/AppFooter.vue";
export default {
  components: {
    AppMain,
    AppFooter,
    AppHeader
},
  data() {
    return {
      store,
    }
  },
  created() {
    axios
    .get ("https://api.themoviedb.org/3/search/movie", {
      params: {
        api_key: this.store.api_key
      }
    })
    .then ((resp) => {
      this.store.myArr = resp.data.results
      console.log(resp.data.results);
    })
    
  },

}
</script>

<template>
  <div>
    <div>
      <h1>{{ store.testElem }}</h1>
    </div>
    <AppHeader />
    <AppMain />
    <AppFooter />
  </div>
</template>

<style lang="scss" scoped>
  
</style>