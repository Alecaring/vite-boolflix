<script>
import axios from 'axios';
import { store } from '../store';
export default {
  data() {
    return {
      store,
    }
  },
  
  methods: {
    sendUserQuery() {
      axios
    .get ("https://api.themoviedb.org/3/search/movie", {
      params: {
        "api_key": this.store.api_key,
        "query": this.store.userQuery,
      }
    })
    .then ((resp) => {
      this.store.myArr = resp.data.results
      console.log(this.store.myArr);
    })
    }
  }
  

}
</script>

<template>
  <div>
    <label for="serchBar">cerca qui</label>
    <input v-model="store.userQuery" type="search" id="serchBar" placeholder="cerca">
  </div>
  <div>
    <button @click="sendUserQuery">premi</button>
  </div>
</template>

<style lang="scss" scoped>
  
</style>