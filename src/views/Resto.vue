<template>
  <div class="home">
    <RestoDetail/>
  </div>
</template>

<script>
// @ is an alias to /src
import RestoDetail from "@/components/RestoDetail.vue";

export default {
  name: "home",
  components: {
    RestoDetail
  }
};
</script>
