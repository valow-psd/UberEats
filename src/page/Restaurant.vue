<template>
    <div>
        <RouterLink to="/">
            <div class="retour-home">
                Retour à l'accueil
            </div>
        </RouterLink>
        <img :src="restaurant.image" alt="">
        <p>{{ restaurant.name }}</p>
        <p>Note : {{ restaurant.note }}</p>
        <p>Livraison : {{ restaurant.drive_time }}</p>
    </div>
</template>

<script>
    import {
        useRoute
    } from "vue-router";
    import BDD from "../BDD";
    export default {
        name: 'restaurant-vue',
        setup() {
            const route = useRoute();
            const restaurant = BDD.find((restaurant) => restaurant.name === route.params.name)
            return {
                restaurant
            }
        }
    }
</script>

<style lang="scss" scoped>
    .retour-home {
        margin-bottom: 25px;
        font-weight: 400;
        cursor: pointer;
        pointer-events: none;
        text-decoration : none!important;
        color: black;

        .retour-home:link { text-decoration: none; }

        .retour-home:visited { text-decoration: none; }

        .retour-home:hover { text-decoration: none; }

        .retour-home:active { text-decoration: none; }

        &:hover{
            font-weight: 900;
        }


    }
</style>