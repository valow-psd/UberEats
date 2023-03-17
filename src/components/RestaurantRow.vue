<template>
  <div class="restaurant--row">
    <h2 class="title">
        Nos Restaurants
    </h2>
    <div class="wrapper--card">
        <RouterLink class="restaurant--wrapper" v-for="(restaurant, index) in three_restaurant" :key="index" :to="{name: 'Restaurant', params: {name: restaurant.name}}">
            <restaurant-card :info_restaurant="restaurant" />
        </RouterLink>
    </div>
    
  </div>
</template>

<script>
import RestaurantCard from './RestaurantCard.vue';

export default {
    name: "RestaurantRow",
    components:{
        RestaurantCard,
    },
    props: {
        three_restaurant: Array
    }
}
</script>

<style lang="scss">
    .restaurant--row{
        .restaurant--wrapper{
            width: 32%;
            text-decoration:none!important;
            color: black;

            
        }
        .wrapper--card{
            display: flex;
            align-items: center;
            justify-content: space-between;
        }
        
    }
</style>