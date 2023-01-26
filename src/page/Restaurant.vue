<template>
    <p>Restaurant</p>
</template>

<script>
import { onMounted } from "vue";
import BDD from "../BDD";
export default {
    name: 'restaurant-vue',
    setup(){
        onMounted(() => {
            console.log(BDD);
        })
    }
}
</script>

<style>

</style>
