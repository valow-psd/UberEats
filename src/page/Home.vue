<template>
  <div class="home-page">
    <div class="header">
      <img src="https://d3i4yxtzktqr9n.cloudfront.net/web-eats-v2/ee037401cb5d31b23cf780808ee4ec1f.svg"
        alt="logo-uber-eats">
      <div class="wrapper--input">
        <input v-model="user_search_restaurant" type="text" placeholder="Plats, nourriture, boissons, ...">
        <div class="search">
          <router-link v-for="(restaurant, i) in search_restaurant" :key="i" :to="{name: 'Restaurant', params: {name: restaurant.name}}">
            <div class="container--restaurant--search">
            <div class="wrapper--img">
              <img :src="restaurant.image" alt="photo-resto">
            </div>
            <p>{{ restaurant.name }}</p>
          </div>
          </router-link>
        </div>
      </div>
    </div>
    <div class="banner">

    </div>
    <RestaurantRow v-for="(data, i) in data_restaurant" :key="i" :three_restaurant="data" />

  </div>

</template>

<script>
  //IMPORTS
  import BDD from '../BDD.js';
  import {
    onMounted,
    ref,
    watch
  } from 'vue';

  //Components
  import RestaurantRow from '@/components/RestaurantRow.vue';
  export default {
    name: 'HomePage',
    components: {
      RestaurantRow,
    },
    setup() {
      class Restaurants {
        constructor(name, note, image, drive_time) {
          this.name = name;
          this.note = note;
          this.image = image;
          this.drive_time = drive_time;
        }
      }

      let data_restaurant = ref([]);
      let all_restaurants = [];

      const makeDatarestaurant = () => {

        let three_restaurants = [];


        for (const restaurant of BDD) {
          const new_restaurant = new Restaurants(restaurant.name, restaurant.note, restaurant.image, restaurant
            .drive_time)

          // tableau avec tous les restos
          all_restaurants.push(new_restaurant);

          if (three_restaurants.length === 2) {
            three_restaurants.push(new_restaurant)
            data_restaurant.value.push(three_restaurants)
            three_restaurants = []
          } else {
            three_restaurants.push(new_restaurant)
          }

        }

        console.log(data_restaurant)
      }

      //Recherche input 
      let user_search_restaurant = ref('');
      let search_restaurant = ref([]);
      watch(user_search_restaurant, new_value => {

        let regex = RegExp(new_value.toLowerCase());

        let new_search_restaurant = all_restaurants.filter(restaurant => regex.test(restaurant.name.toLowerCase()));

        new_value === "" ? search_restaurant.value = [] : search_restaurant.value = new_search_restaurant;


      })

      onMounted(makeDatarestaurant)

      //return
      return {
        user_search_restaurant,
        data_restaurant,
        search_restaurant
      }
    }
  }
</script>

<style lang="scss">
  .home-page {
    .header {
      height: 120px;
      width: 100%;
      display: flex;
      align-items: center;
      justify-content: space-between;


      img {
        width: 150px;
      }

      .wrapper--input {
        position: relative;

        input {
          background-color: #f6f6f6;
          border: none;
          height: 60px;
          width: 400px;
          outline: none;
          padding-left: 20px;
        }

        .search {
          position: absolute;
          top: 100%;
          width: 100%;
          /*height: 400px;*/
          background-color: #fff;
          border-radius: 5%;
          box-shadow: rgba(50, 50, 93, 0.25) 0px 50px 100px -20px, rgba(0, 0, 0, 0.3) 0px 30px 60px -30px;
          /*border: solid 1px red;*/

          .container--restaurant--search {
            display: flex;
            align-items: center;
            padding: 10px;

            &:hover {
              background-color: #f6f6f6;
            }

            .wrapper--img {
              height: 60px;
              width: 60px;
              margin-right: 25px;
              border-radius: 50%;
              overflow: hidden;

              img {
                height: 100%;
                width: auto;
              }
            }
          }
        }
      }

    }

    .banner {
      height: 200px;
      width: 100%;
      background-image: url(https://www.uber-assets.com/image/upload/f_auto,q_auto:eco,c_fill,w_945,h_532/v1622579097/assets/6a/090a5b-1c9a-48ed-97b1-f89e7285edc8/original/20190426_UberEats-Wokano_%28c%29AudreyMa_0079.jpg);
      background-size: cover;
      background-position: center center;
    }
  }
</style>