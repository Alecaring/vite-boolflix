<script>
import axios from 'axios';
import { store } from '../store';
import "@fortawesome/fontawesome-free/css/all.css";


export default {
    data() {
        return {
            store,
            flagFromApi: [],
            flagFromObj: [],
            flagImg: [],
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
        getFlagUrl(code) {
            const flagMap = {
                'it': 'https://upload.wikimedia.org/wikipedia/commons/thumb/0/03/Flag_of_Italy.svg/2560px-Flag_of_Italy.svg.png',
                'fr': 'https://upload.wikimedia.org/wikipedia/commons/thumb/c/c3/Flag_of_France.svg/2560px-Flag_of_France.svg.png',
                'en': 'https://upload.wikimedia.org/wikipedia/commons/thumb/a/a4/Flag_of_the_United_States.svg/1280px-Flag_of_the_United_States.svg.png',
                'zh': 'https://www.officine-vimercati.it/imgs/1109/Bandiera_ZH.jpeg?s=large',
                'ru': 'https://upload.wikimedia.org/wikipedia/commons/thumb/f/f3/Flag_of_Russia.svg/1280px-Flag_of_Russia.svg.png',
                "ja": "https://upload.wikimedia.org/wikipedia/commons/thumb/0/0a/Flag_of_Jamaica.svg/1280px-Flag_of_Jamaica.svg.png",
                "pt": "https://upload.wikimedia.org/wikipedia/commons/thumb/5/5c/Flag_of_Portugal.svg/2560px-Flag_of_Portugal.svg.png",
                "ml": "https://upload.wikimedia.org/wikipedia/commons/thumb/6/66/Flag_of_Malaysia.svg/2560px-Flag_of_Malaysia.svg.png",
                "es": "https://flagpedia.net/data/flags/w1600/es.png",
                "no": "https://wiki.art-decor.org/images/1/1e/Flag_no.svg",
                "vi": "https://upload.wikimedia.org/wikipedia/commons/thumb/2/21/Flag_of_Vietnam.svg/1280px-Flag_of_Vietnam.svg.png",
                "ko": "https://upload.wikimedia.org/wikipedia/commons/thumb/0/09/Flag_of_South_Korea.svg/800px-Flag_of_South_Korea.svg.png",


            };
            return flagMap[code] || "https://upload.wikimedia.org/wikipedia/commons/thumb/f/f3/Flag_of_Russia.svg/1280px-Flag_of_Russia.svg.png";
        },
        getPosterUrl(path) {
            const baseUrl = "https://image.tmdb.org/t/p/w500";
            return path ? `${baseUrl}${path}` : '';
        },




        // DATI:
        // massimo numero di stelle 5


        // SUPPOSIZIONE:  

        // ho 3 stelle piene 
        // ho 2 stelle vuote
        getDataByStars(data) {
            let maxStars = 5; // massimo di stelle
            let stars = Math.ceil(data / 2); // diventa 5 da 10
            let fullStars = stars; // paragoniamo le stelle piene al voto del film
            let emptyStars = maxStars - stars; // facciamo la differenza tra il massimo di stelle e i voti del film
            return {
                full: fullStars,
                empty: emptyStars
            }
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
                    <img :src="getPosterUrl(myItem.poster_path)" :alt="myItem.original_title" loading="lazy">
                    <div class="hover">
                        <div class="TopHover">
                            <h2 class="headerHover">{{ myItem.original_title }}</h2>
                        </div>
                        <div class="bottomHover">
                            <span>
                                {{ getDataByStars(myItem.vote_average) }}
                            </span>
                            <span class="containerFlag">
                                <img :src="getFlagUrl(myItem.original_language)" :alt="myItem.original_title"
                                    loading="lazy">
                            </span>






                            <div class="stars">
                                <!-- stella piena -->
                                <i class="fa-solid fa-star"></i>
                               
                                <!-- stella vuota -->
                                <i class="fa-regular fa-star"></i>
                            </div>





                        </div>
                    </div>
                </div>


            </div>


        </div>
    </div>
</template>

<style lang="scss" scoped>

.stars {
    background-color: transparent;

    i {
        background-color: transparent;
    }
}
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
            background-color: transparent;

            input {
                width: 80%;
                height: 100%;
                padding: 2vw;
                font-size: 2vw;
                color: red;
                background-color: transparent;
                border: .1px solid white;
                outline: none;


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
                position: relative;
                width: calc(100% / 3 - 10px);
                height: 40vh;
                overflow: hidden;


                img {
                    width: 100%;
                    height: 100%;
                    object-fit: cover;

                    &:hover {
                        opacity: 1;
                    }
                }

                &:hover .hover {
                    position: absolute;
                    top: 50%;
                    left: 50%;
                    transform: translate(-50%, -50%);
                    z-index: 1000;
                    width: 101%;
                    height: 101% !important;
                    background-color: #00000086;


                    object-fit: cover;

                    .TopHover {
                        position: absolute;
                        top: 0;
                        width: 100%;
                        height: 30%;
                        background-color: #ffffff00;

                        .headerHover {
                            border-left: 5px solid red;
                            width: 90%;
                            font-size: 1vw;
                            margin: .2vw auto;
                            background-color: #ffffff00;
                            color: #ffffff;
                        }
                    }

                    .bottomHover {
                        display: flex;
                        justify-content: space-between;
                        align-items: center;
                        position: absolute;
                        bottom: 0;
                        width: 100%;
                        height: 30%;
                        background-color: transparent;

                        .containerFlag {
                            height: 40%;
                            width: auto;

                            overflow: hidden;
                            background-color: transparent;

                            img {
                                width: 100%;
                                height: 100%;
                                object-fit: cover;
                            }
                        }

                        span {
                            color: white;
                            margin: 0 1vw;
                        }

                    }
                }
            }
        }

    }
}
</style>