<template>
  <div class="home">
    <RestoList msg="List of Restaurant from zomato"/>
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
