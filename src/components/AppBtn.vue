<script>
import { store } from '../store';
export default {
  data() {
    return {
      store,
    }
  },
  methods: {
    userQuery() {

      this.store.userQuery = this.store.userQuery;
      console.log(this.store.paramsQuery);
      console.log(this.store.myArr);
    }
  },
}
</script>

<template>
  
</template>

<style lang="scss" scoped>
  
</style>