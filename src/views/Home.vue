<template>
  <div class="home">
    <Streams />
  </div>
</template>

<script>
// @ is an alias to /src
import Streams from "@/components/Streams.vue";

export default {
  name: "Home",
  components: {
    Streams,
  },
};
</script>
<style scoped>
@media (max-width: 1200px) {
  img {
    display: block;
  }
}
</style>
