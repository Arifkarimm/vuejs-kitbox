<template>
  <div>
    <h2>NewList</h2>
    <ul>
      <li v-for="result in results" :key="result.id">{{ result.brand }} - {{ result.name }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "NewList",
  props: ["results"]
};
</script>

<style scoped>
</style>