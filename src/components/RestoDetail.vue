<template>
    <div>
        <main>
            <h4>Here's your Choosen Restaurant</h4>
            <h1 class="mb-4">{{ $route.params.rname }}</h1>
            <button class="btn btn-primary mb-1" @click="getMenu">Get Daily Menu</button>
            <br>
            <router-link to="/resto" class="btn btn-warning mb-5">Go Back</router-link>
            <p>Daily menu status: <strong> {{msg}}</strong></p>
            <div class="wrapper">
                <div class="container">
                    <div class="row">
                        <div v-for="menu in menus" :key="menu.dish.dish_id" class="col-md-4 p-2">
                            <div class="card">
                                <div class="card-body">
                                    <h5 class="card-title">{{ menu.dish.id }}</h5>
                                    <p class="card-text"><strong> {{ menu.dish.name }}.</strong></p>
                                    <p class="card-text" v-if="menu.dish.price==''">price is empty.</p>
                                    <p class="card-text" v-else>{{ menu.dish.price }}.</p>
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
            menus: [],
            msg : 'Request Status'
        }
    }, 
    methods: {
        getMenu: function () {
            axios.get("https://developers.zomato.com/api/v2.1/dailymenu",{
                headers: {
                    'user-key' : '854aacf9e97a3c22d45d7876687cf249'
                },
                params: {
                    'res_id' : this.$route.params.id
                }
            })
            .then((response)  =>  {
                this.menus = response.data.daily_menus[0].daily_menu.dishes;
                console.log("success");
                this.msg = "Menu Available";
            }, (error)  =>  {
                console.log(error);
                this.msg = "Menu not Found, Please choose another restaurant";
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

