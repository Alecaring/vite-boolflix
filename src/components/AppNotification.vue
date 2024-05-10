<script>
import { store } from '../store'
export default {
    data() {
        return {
            store,
            activeIndex: 0,
            intervalId: null,
            
        }
    },
    
    methods: {
        getPosterUrl(path) {
            const baseUrl = "https://image.tmdb.org/t/p/w500";
            return path ? `${baseUrl}${path}` : '';
        },
        getRandomNum() {
            this.activeIndex = Math.floor(Math.random() * 20);
        }
    },
    mounted() {
        this.intervalId = setInterval(this.getRandomNum, 3000)

    }
}
</script>

<template>
    <div v-if="store.ArrayCorrispondIdHome && store.ArrayCorrispondIdHome.length > 0" class="containerBanner">
        <img :src="getPosterUrl(store.ArrayCorrispondIdHome[activeIndex]?.backdrop_path)" alt="">
        <div class="hoverContainerBanner">
            <h2 class="headingInnerBanner"><strong>N</strong>etflix Selection</h2>
            <h2 class="BottomInnerBanner">{{ store.ArrayCorrispondIdHome[activeIndex]?.original_title }}</h2>
        </div>
    </div>
</template>

<style lang="scss" scoped>
    .containerBanner {
        position: relative;
        background-color: rgb(0, 0, 0);
        width: 100%;
        height: 60vh;
        color: white;
        img {
            width: 100%;
            height: 100%;
            opacity: .6;
            object-fit: cover;
        }
        .hoverContainerBanner {
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            position: absolute;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: transparent;
            box-shadow: inset 0px 20px 20px 5px #000000e6;
            .headingInnerBanner {
                margin: 3vw;
                font-size: 5vw;
                padding: 0 2vw;
                background-color: transparent;
                border-left: 3px solid red;
                letter-spacing: 5px;
                strong {
                    background-color: transparent;
                    color: red;
                }
            }
            .BottomInnerBanner {
                background-color: transparent;
                margin: 3vw;
                font-size: 5vw;
                padding: 0 2vw;
            }
        }
    }
</style>