<script>
import { store } from '../store';
export default {
    data() {
        return {
            store,
            txtGeneratedBySearch: "Risultati",
            alessio: true,
        }
    },
    methods: {
        // Restituisce l'URL completo per l'immagine del poster
        getPosterUrl(path) {
            const baseUrl = "https://image.tmdb.org/t/p/w500";
            return path ? `${baseUrl}${path}` : '';
        }
    }

}
</script>

<template>
    <div class="container">
        <div class="InnerTitleContainer">
            <h1 :class="store.myArr.length >= 1 ? 'block' : 'none'"> con "{{ store.userQuery }}"</h1>
        </div>
        <div class="ContainerCard">
            <div v-for="myItem in store.myArr" class="card">
                <img :src="getPosterUrl(myItem.poster_path)" alt="">
                <h1>{{ myItem.id }}</h1>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>
.container {
    height: 90vh;
    background-color: #795454;
    overflow: auto;

    .InnerTitleContainer {
        width: 100%;
        padding: 4vw;
        color: white;
    }

    .ContainerCard {
        display: flex;
        flex-wrap: wrap;
        justify-content: flex-start;
        gap: 30px;
        width: 100%;
    }

    .card {
        width: 30vw;
        height: 25vh;

        background-color: #fff;
        overflow: hidden;

        img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
    }
}

.block {
    display: block;
}

.none {
    display: none;
}
</style>