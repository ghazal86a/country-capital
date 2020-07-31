<template>
  <div class="home">
    <Country />
  </div>
</template>

<script>
// @ is an alias to /src
import Country from "@/components/Country.vue";

export default {
  name: "Home",
  components: {
    Country
  }
};
</script>
