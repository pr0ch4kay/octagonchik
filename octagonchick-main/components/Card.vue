
<template>
  <div class="card">
    <h2>{{ data.title }}</h2>
    <p class="category">{{ data.category }}</p>
    <p class="location">{{ data.location }}</p>
    <p class="address">{{ data.address }}</p>
    <p class="age">{{ data.age }}</p>
    <p class="price">{{ data.price }}</p>
  </div>
</template>

<script setup>
defineProps({
  data: Object
});
</script>

<style scoped>
.card {
  background-color: #fff;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  padding: 20px;
  margin-bottom: 20px;
}

.category {
  font-weight: bold;
  color: #555;
}

.location,
.address,
.age,
.price {
  color: #777;
  font-size: 14px;
}
</style>
