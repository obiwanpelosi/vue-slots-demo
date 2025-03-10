<script setup>
const props = defineProps({
  count: Number,
});
</script>
<template>
  <section>
    <h1>My incredible list of {{ count }} users</h1>
  </section>
</template>

<style scoped>
section {
  background-color: #f0f0f0;
  padding: 20px;
  border-radius: 5px;
  margin: 20px 0;
}
h1 {
  color: #333;
}
</style>
