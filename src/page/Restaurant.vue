<template>
    <p>a{{ $route.params.name }}</p>
</template>

<script>
import { onMounted } from "vue";
import { useRoute } from "vue-router";
import BDD from "../BDD";
export default {
    name: 'restaurant-vue',
    setup(){
        const route = useRoute();
        onMounted(() => {
            BDD.find((restaurant) => {
                if(restaurant.name === route.params.name){
                    return restaurant;
                }
            } )
        })
    }
}
</script>

<style>

</style>
