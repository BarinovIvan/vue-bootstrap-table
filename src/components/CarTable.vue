<template>
  <table class="table table-striped table-bordered">
    <thead>
    <tr>
      <th scope="col" class="w-25">ID</th>
      <th scope="col" class="w-50">Brand</th>
      <th scope="col" class="w-50">Year</th>
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
