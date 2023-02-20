<template>
  <div class="container">
    <div class="search-area">
      <CustomSearch
          @start-searching="$emit('start-searching', $event)"
          @stop-searching="$emit('stop-searching')"
          text-placeholder="ID"
      />
      <CustomSearch
          @start-searching="$emit('start-searching', $event)"
          @stop-searching="$emit('stop-searching')"
          text-placeholder="Brand"
      />
      <CustomSearch
          @start-searching="$emit('start-searching', $event)"
          @stop-searching="$emit('stop-searching')"
          text-placeholder="Age"
      />
    </div>
    <car-table :cars="cars"/>
  </div>
</template>

<script setup>
  import CarTable from "@/components/CarTable";
  import CustomSearch from "@/components/CustomSearch";

  const cars = [
    {id: 1, brand: 'BMW', age: 2010},
    {id: 2, brand: 'Audi', age: 2012},
    {id: 3, brand: 'BMW', age: 2016},
    {id: 4, brand: 'Audi', age: 2018},
    {id: 4, brand: 'Mercedes', age: 2018},
    {id: 4, brand: 'Mercedes', age: 2017},
    {id: 4, brand: 'Mercedes', age: 2016},
    {id: 4, brand: 'Audi', age: 2018},
    {id: 4, brand: 'BMW', age: 2010},
  ]

  const carsSortedList = computed(() => someReactiveRef.value)

</script>

<style lang="scss">
  .search-area {
    display: flex;
    gap: 20px;
    justify-content: center;
    margin: 20px 0;
  }
</style>
