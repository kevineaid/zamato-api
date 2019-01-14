<template>
    <div>
        <main>
            <h2 class="mb-5">List of Restaurant from zomato (Praha 10 - Czech)</h2>
            <button id="btn" class="btn btn-primary mb-5" v-on:click="getRestaurant">Get Restaurant</button>

            <div v-if="loading">
            <img src="../assets/496.gif"/>
            
            </div>

            <div class="wrapper">
                <div class="container">
                    <div class="row">
                        <div v-for="resto in restaurants" :key="resto.restaurant.collection_id" class="col-md-4 p-2">
                            <div class="card">
                                <img class="card-img-top"  alt="Card image cap"  v-bind:src="resto.restaurant.featured_image" />
                                <div class="card-body">
                                    <h5 class="card-title">{{ resto.restaurant.name }}</h5>
                                    <h5>id {{resto.restaurant.id}}</h5>
                                    <p class="card-text">Cuisines : {{ resto.restaurant.cuisines }}.</p>
                                    <router-link :to="{ name: 'restoDetail', params: {id: resto.restaurant.id, rname: resto.restaurant.name }}" class="btn btn-primary">Choose</router-link>
                                </div>
                                
                                
                            </div>                         
                        </div>
                    </div>

                </div>
            </div>
        </main>
    </div>
</template>

<script>
import axios from 'axios';
  
export default {
    name: 'app',
    data () {
        return {
            restaurants: [],
            loading: false
        }
    }, 
    methods: {
        getRestaurant: function () {
            this.loading = true;
            axios.get("https://developers.zomato.com/api/v2.1/search",{
                headers: {
                    'user-key' : '854aacf9e97a3c22d45d7876687cf249'
                },
                params: {
                    'entity_id' : 84,
                    'entity_type' : 'city',
                    'count' : 100,
                    'sort' : 'rating',
                    'order' : 'asc'
                }
            })
            .then((response)  =>  {
                this.loading = false;
                this.restaurants = response.data.restaurants;
                console.log("success");
            }, (error)  =>  {
                this.loading = false;
                console.log(error);
            })
        }
    },
}
</script>
<style>
.resto-cards {
    border: 1px solid #aaa;
    border-radius: 4px;
    padding: 10px;
}   
</style>

