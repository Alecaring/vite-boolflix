<script>
import { store } from "../src/store";
import axios from "axios";
import AppHeader from "./components/AppHeader.vue";
import AppMain from "./components/AppMain.vue";
export default {
  components: {
    AppMain,
    AppHeader
},
  data() {
    return {
      store,
    }
  },
  created() {

    
  },
  methods: {
    
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
    
  </div>
</template>

<style lang="scss" scoped>
  
</style>