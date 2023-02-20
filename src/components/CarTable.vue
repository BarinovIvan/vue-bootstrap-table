<template>
  <table class="table table-striped table-bordered">
    <thead>
    <tr>
      <th scope="col">ID</th>
      <th scope="col">Brand</th>
      <th scope="col">Year</th>
    </tr>
    </thead>
    <tbody>
      <CarInfoRow
        v-for="carInfo in cars"
        :key="carInfo.id"
        :carInfo="carInfo"
      />
    </tbody>
  </table>
</template>

<script setup>
  import CarInfoRow from "@/components/CarInfoRow";

  defineProps(['cars'])
</script>

<style scoped>

</style>