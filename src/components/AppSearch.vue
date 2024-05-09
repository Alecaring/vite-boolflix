<script>
import axios from 'axios';
import { store } from '../store';


export default {
    data() {
        return {
            store,
        }
    },

    created() {
        this.sendUserQuery();
        this.sendUserList();
    },

    methods: {
        sendUserQuery() {
            axios
                .get("https://api.themoviedb.org/3/search/movie", {
                    params: {
                        "api_key": this.store.api_key,
                        "query": this.store.userQuery,
                    }
                })
                .then((resp) => {
                    this.store.myArr = resp.data.results
                    console.log(this.store.myArr);
                })
        },
        sendUserList() {
            axios
                .get("https://api.themoviedb.org/3/genre/movie/list", {
                    params: {
                        "api_key": this.store.api_key,
                    }
                })
                .then((resp) => {
                    this.store.ArrayTitleHome = resp.data.genres

                })
        },
        getPosterUrl(path) {
            const baseUrl = "https://image.tmdb.org/t/p/w500";
            return path ? `${baseUrl}${path}` : '';
        }
    }



}
</script>

<template>
    <div class="container">
        <div class="sidebarLeft">

            <div class="StyleInput">
                <input aria-label="serchBar" v-model="store.userQuery" type="search" id="serchBar" placeholder="cerca">
                <button @click="sendUserQuery"><span><svg xmlns="http://www.w3.org/2000/svg" width="2.5vw" height="2.5vw"
                            fill="currentColor" class="bi bi-search-heart-fill" viewBox="0 0 16 16">
                            <path
                                d="M6.5 13a6.47 6.47 0 0 0 3.845-1.258h-.001q.044.06.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1 1 0 0 0-.115-.1A6.47 6.47 0 0 0 13 6.5 6.5 6.5 0 0 0 6.5 0a6.5 6.5 0 1 0 0 13m0-8.518c1.664-1.673 5.825 1.254 0 5.018-5.825-3.764-1.664-6.69 0-5.018" />
                        </svg></span></button>
            </div>
            <div class="containerListSuggestions">
                <div class="containerTxt">
                    <h2>I Più Cercati :</h2>
                </div>
                <ul>
                    <li v-for="item in store.ArrayTitleHome">
                        {{ item.name }}
                    </li>
                </ul>
            </div>
        </div>
        <div class="sidebarRight">
            <div class="containerCard">
                <h2>{{ store.myArr.length }} Risultati Generati con '{{ store.userQuery }}' .</h2>
                <div v-for="myItem in store.myArr" class="card">
                    <img :src="getPosterUrl(myItem.poster_path)" alt="">
                </div>

            </div>


        </div>
    </div>
</template>

<style lang="scss" scoped>
.container {
    position: relative;
    width: 100%;
    height: 90vh;
    background-color: rgba(0, 0, 0, 0.851);

    .sidebarLeft {
        position: absolute;
        left: 0;
        width: 35vw;
        height: 100%;
        background-color: black;

        .StyleInput {
            display: flex;
            align-items: center;
            width: 100%;
            height: 10vh;
            background-color: #fff;

            input {
                width: 80%;
                height: 100%;
                padding: 2vw;
                font-size: 2vw;
                color: red;
                border: .1px solid white;
            }

            button {
                width: 20%;
                height: 100%;
                margin: 0;
                padding: 0;
                border: 0;
                box-shadow: none;
                background-color: #fff;

                span {
                    background-color: #fff;

                    svg {
                        background-color: #fff;
                    }
                }
            }
        }

        .containerListSuggestions {
            width: 100%;
            height: 80vh;
            overflow: auto;

            .containerTxt {
                margin: 3vw 2vw 0;
                font-size: 2vw;
                color: white;
            }


            ul {
                list-style-type: none;
                padding: 3vw 1vw 0;

                li {
                    padding: 1.5vw 2.5vw;
                    margin: 0.5vw 0;
                    color: #fff;
                    font-size: 1.5vw;
                    background-color: #ffffff1b;
                    border: 1px solid black;
                    border-radius: 2rem 2rem 0 0;
                }
            }
        }
    }

    .sidebarRight {
        position: absolute;
        right: 0;
        width: 64vw;
        height: 100%;
        background-color: #000000;
        display: flex;
        justify-content: center;
        align-items: center;

        .containerCard {
            width: 90%;
            height: 95%;
            display: flex;
            flex-wrap: wrap;
            flex-direction: row;
            justify-content: flex-start;
            align-self: start;
            overflow: scroll;
            gap: 10px;

            h2 {
                width: 100%;
                color: #ffffff;
                padding: 2vw;
            }

            .card {
                width: calc(100% / 3 - 10px);
                height: 20vh;
                overflow: hidden;

                img {
                    object-fit: cover;
                }

            }
        }

    }
}</style>