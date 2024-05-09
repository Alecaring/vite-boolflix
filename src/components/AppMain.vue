<script>
import { store } from '../store';
import AppHeader from './AppHeader.vue';
import AppCard from './AppCard.vue';
import AppHome from './AppHome.vue';
import AppNewFAmous from './AppNewFAmous.vue';
import AppFilms from "./AppFilms.vue";
import AppMyList from './AppMyList.vue';
import AppSeries from "./AppSeries.vue";
import AppSearch from './AppSearch.vue';
import AppNotifcation from "./AppNotification.vue"

export default {
  components: { AppHeader, AppCard, AppHome, AppNewFAmous, AppFilms, AppMyList, AppSeries, AppSearch, AppNotifcation },
  data() {
    return {
      store,
    }
  },
  methods: {
    alessio() {

    }
  }
}
</script>

<template>
  
  <div>
    <!-- <AppCard /> -->
  </div>
  <div>
    <AppHome v-if="store.activeComponent === 'AppHome'" />
    <AppNewFAmous v-else-if="store.activeComponent === 'AppNewFAmous'" />
    <AppFilms v-else-if="store.activeComponent === 'AppFilms'" />
    <AppMyList v-else-if="store.activeComponent === 'AppMyList'" />
    <AppSeries v-else-if="store.activeComponent === 'AppSeries'" />
    <AppSearch v-else-if="store.activeComponent === 'AppSearch'" />
    <AppNotifcation v-else-if="store.activeComponent === 'AppNotifcation'" />
  </div>
</template>

<style lang="scss" scoped></style>