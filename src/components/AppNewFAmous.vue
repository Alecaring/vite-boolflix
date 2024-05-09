<script>
import { store } from '../store';

export default {
    data() {
        return {
            store,
        }
    },
}
</script>

<template>
    <div class="container">

        <h1>Nuovi e Popolari</h1>

        <div class="collection">
        </div>
        <h1>collection</h1>

        <div class="collection">
        </div>
        <h1>collection</h1>

        <div class="collection">
        </div>

    </div>
</template>

<style lang="scss" scoped>
.container {
    width: 100%;
    height: 90vh;
    background-color: rgb(0, 0, 0);
    overflow: auto;
    h1 {
        color: white;
        padding: 1vw 2vw;
        font-size: 3vw;
    }
    .collection {
        width: 100%;
        height: 30vh;
        background-color: #fff;
    }
}
</style>