<script>
import { store } from '../store'
import axios from 'axios'
export default {
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
                .get("https://api.themoviedb.org/3/genre/tv/list", {
                    params: {
                        "api_key": this.store.api_key,
                    }
                })
                .then((resp) => {
                    this.store.ArrayTitleHome = resp.data.genres

                })
        },
        sendCollectionHome() {
            axios
                .get("https://api.themoviedb.org/3/discover/tv", {
                    params: {
                        "api_key": this.store.api_key,
                    }
                })
                .then((resp) => {
                    this.store.ArrayCorrispondIdHome = resp.data.results
                    console.log(this.store.ArrayCorrispondIdHome);
                })
        },
        getMoviesByGenre(genreId) {
            return this.store.ArrayCorrispondIdHome.filter(film => film.genre_ids.includes(genreId));
        },
        getPosterUrl(path) {
            const baseUrl = "https://image.tmdb.org/t/p/w500";
            return path ? `${baseUrl}${path}` : '';
        },

    }
}
</script>

<template>
    <div class="container">

        <h1 class="Int">Serie TV</h1>
        <div v-for="item in store.ArrayTitleHome">
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
        /* Assicurati che il contenitore abbia una larghezza definita */
        height: 45vh;
        overflow-x: scroll;
        /* Attiva lo scorrimento orizzontale */
        align-items: center;

        .cardCollection {
            min-width: 20vw;
            /* Larghezza minima per ciascun elemento */
            height: 45vh;
            background-color: lightblue;
            text-align: center;
            line-height: 30vh;
            /* Allinea il testo verticalmente */
            overflow: hidden;

            img {
                width: 20vw;
                height: 45vh;
                object-fit: cover;
            }


        }
    }
}
</style>