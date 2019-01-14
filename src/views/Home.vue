<template>
  <div class="home">
    <h1>Simple Resto App</h1>
    <router-link to="/resto" class="btn btn-primary">Go to Restaurant List</router-link>
  </div>
</template>

<script>
// @ is an alias to /src
import RestoList from "@/components/RestoList.vue";

export default {
  name: "home",
  components: {
    RestoList
  }
};
</script>
