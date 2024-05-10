<script>
import { store } from '../store';
import axios from 'axios';
import AppNotification from "./AppNotification.vue";

export default {
    components: {
        AppNotification
    },
    data() {
        return {
            store,
        }
    },
    created() {
        this.sendUserQuery();
        this.sendCollectionHome();
    },
    methods: {
        sendUserQuery() {
            axios
                .get("https://api.themoviedb.org/3/genre/movie/list", {
                    params: {
                        "api_key": this.store.api_key,
                    }
                })
                .then((resp) => {
                    this.store.ArrayTitleHome = resp.data.genres;
                });
        },
        sendCollectionHome() {
            axios
                .get("https://api.themoviedb.org/3/discover/movie", {
                    params: {
                        "api_key": this.store.api_key,
                    }
                })
                .then((resp) => {
                    this.store.ArrayCorrispondIdHome = resp.data.results;
                });
        },
        getMoviesByGenre(genreId) {
            // Filtra i film per genere
            return this.store.ArrayCorrispondIdHome.filter(film => film.genre_ids.includes(genreId));
        },
        getPosterUrl(path) {
            const baseUrl = "https://image.tmdb.org/t/p/w500";
            return path ? `${baseUrl}${path}` : '';
        }
    },
    computed: {
        filteredGenres() {
            // Mostra solo i generi che hanno almeno un film
            return this.store.ArrayTitleHome.filter(genre => this.getMoviesByGenre(genre.id).length > 4);
        }
    }
}
</script>

<template>
    <div class="container">
        <h1 class="Int">Home</h1>
        <AppNotification />
        <!-- Utilizza la proprietà computata `filteredGenres` per filtrare i generi -->
        <div v-for="item in filteredGenres" :key="item.id">
            <h1>{{ item.name }}</h1>
            <div class="collection">
                <div v-for="film in getMoviesByGenre(item.id)" :key="film.id" class="cardCollection">
                    <img :src="getPosterUrl(film.poster_path)" :alt="item.name" loading="lazy" />
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>
.container {
    width: 100%;
    height: 90vh;
    background-color: rgb(0, 0, 0);
    overflow: auto;

    .Int {
        font-size: 3vw;
    }

    h1 {
        color: white;
        padding: 1vw 2vw;
        font-size: 2vw;
    }

    .collection {
        display: flex;
        flex-direction: row;
        flex-wrap: nowrap;
        gap: 10px;
        width: 100%;
        height: 45vh;
        overflow-x: scroll;
        align-items: center;

        .cardCollection {
            min-width: 20vw;
            height: 45vh;
            background-color: lightblue;
            text-align: center;
            overflow: hidden;

            img {
                width: 100%;
                height: 100%;
            }
        }
    }
}
</style>
