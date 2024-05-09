<script>
import { store } from '../store';
import AppSearchBar from './AppSearchBar.vue';

export default {
  components: { AppSearchBar },
  data() {
    return {
      store,
    }
  },
  methods: {
    setActiveComponent(component) {
      // Assegna il valore direttamente alla proprietà dello store
      store.activeComponent = component;
      console.log(store.activeComponent);
    }
  }
}
</script>

<template>
  <div class="container">

    <ul class="prima">
      <li>
        <img
          src="https://static.vecteezy.com/system/resources/previews/020/190/493/non_2x/netflix-logo-netflix-icon-free-free-vector.jpg"
          alt="">
      </li>
      <li @click="setActiveComponent('AppHome')">Home</li>
      <li @click="setActiveComponent('AppSeries')">Serie TV</li>
      <li @click="setActiveComponent('AppFilms')">Film</li>
      <li @click="setActiveComponent('AppNewFAmous')">Nuovi e popolari</li>
      <li @click="setActiveComponent('AppMyList')">La mia lista</li>
    </ul>

    <ul class="seconda">
      <li @click="setActiveComponent('AppSearch')">
        
        <svg xmlns="http://www.w3.org/2000/svg" width="2vw" height="2vw" fill="currentColor" class="bi bi-search"
          viewBox="0 0 16 16">
          <path
            d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001q.044.06.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1 1 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0" />
        </svg>
      </li>
      <li @click="setActiveComponent('AppNotifcation')">
        <svg xmlns="http://www.w3.org/2000/svg" width="2vw" height="2vw" fill="currentColor" class="bi bi-bell-fill"
          viewBox="0 0 16 16">
          <path
            d="M8 16a2 2 0 0 0 2-2H6a2 2 0 0 0 2 2m.995-14.901a1 1 0 1 0-1.99 0A5 5 0 0 0 3 6c0 1.098-.5 6-2 7h14c-1.5-1-2-5.902-2-7 0-2.42-1.72-4.44-4.005-4.901" />
        </svg>
      </li>
      <li>
        <svg xmlns="http://www.w3.org/2000/svg" width="2vw" height="2vw" fill="rgb(164, 164, 246)"
          class="bi bi-people-fill" viewBox="0 0 16 16">
          <path
            d="M7 14s-1 0-1-1 1-4 5-4 5 3 5 4-1 1-1 1zm4-6a3 3 0 1 0 0-6 3 3 0 0 0 0 6m-5.784 6A2.24 2.24 0 0 1 5 13c0-1.355.68-2.75 1.936-3.72A6.3 6.3 0 0 0 5 9c-4 0-5 3-5 4s1 1 1 1zM4.5 8a2.5 2.5 0 1 0 0-5 2.5 2.5 0 0 0 0 5" />
        </svg>
      </li>
    </ul>

  </div>
</template>

<style lang="scss" scoped>
.container {
  width: 100%;
  height: 10vh;
  background-color: black;
  display: flex;
  justify-content: space-between;
  align-items: center;


  .prima {
    list-style-type: none;
    display: flex;
    justify-content: flex-start;
    align-items: center;
    height: 100%;

    li {
      color: white;
      padding: 0 1vw;

      img {
        width: 10vw;
      }

      ul {
        li {
          color: white;
        }
      }
    }
  }

  .seconda {
    color: white;
    display: flex;
    list-style-type: none;

    li {
      padding: 0 2vw;
    }

  }
}
</style>