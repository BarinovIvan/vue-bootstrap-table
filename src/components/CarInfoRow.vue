<template>
  <tr>
    <th scope="row">{{ carInfo.id }}</th>
    <td>{{ carInfo.brand }}</td>
    <td>{{ carInfo.age }}</td>
  </tr>
</template>

<script setup>
  defineProps(['carInfo'])
</script>

<style scoped>

</style>