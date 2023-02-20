<template>
  <div class="container">
    <div class="search-area">
      <CustomSearch
          @start-searching="setIdSearch($event)"
          @stop-searching="clearIdSearch()"
          text-placeholder="ID"
      />
      <CustomSearch
          @start-searching="setBrandSearch($event)"
          @stop-searching="clearBrandSearch()"
          text-placeholder="Brand"
      />
      <CustomSearch
          @start-searching="setAgeSearch($event)"
          @stop-searching="clearAgeSearch()"
          text-placeholder="Age"
      />
      <CustomDatePicker title="Start:" />
      <CustomDatePicker title="End:" />
    </div>
    <car-table :cars="filteredCarList"/>
  </div>
</template>

<script setup>
import CarTable from "@/components/CarTable";
import CustomSearch from "@/components/ui/CustomSearch";
import {computed, reactive, ref} from "vue";
import CustomDatePicker from "@/components/ui/CustomDatePicker";

let searchQuery = reactive({})

  const cars = [
    { id: 1, brand: 'BMW', age: 2010 },
    { id: 2, brand: 'Audi', age: 2012 },
    { id: 3, brand: 'BMW', age: 2016 },
    { id: 4, brand: 'Audi', age: 2018 },
    { id: 5, brand: 'Mercedes', age: 2018 },
    { id: 6, brand: 'Mercedes', age: 2017 },
    { id: 7, brand: 'Mercedes', age: 2016 },
    { id: 8, brand: 'Audi', age: 2018 },
    { id: 9, brand: 'BMW', age: 2010 },
  ]


  function setIdSearch(id) {
    searchQuery.id = id
    console.log(searchQuery)
  }
  function clearIdSearch() {
    delete searchQuery.id
  }

  function setBrandSearch(brand) {
    searchQuery.brand = brand
    console.log(searchQuery)
  }
  function clearBrandSearch() {
    delete searchQuery.brand
  }

  function setAgeSearch(age) {
    searchQuery.age = age
    console.log(searchQuery)
  }
  function clearAgeSearch() {
    delete searchQuery.age
  }

  const filteredCarList = computed(() => {
    return cars.filter(car => {
      switch (Object.values(searchQuery).length) {
        case 0:
          return cars;
        case 1:
          return car.id.toString().includes(searchQuery.id)
              || car.brand?.toLowerCase().includes(searchQuery.brand?.toLowerCase())
              || car.age.toString().includes(searchQuery.age);
        case 2:
          if (searchQuery.id) {
            if (searchQuery.brand) {
              return car.id.toString().includes(searchQuery.id)
                  && car.brand?.toLowerCase().includes(searchQuery.brand?.toLowerCase())
            } else {
              return car.id.toString().includes(searchQuery.id)
                  && car.age.toString().includes(searchQuery.age);
            }
          } else {
            return car.brand?.toLowerCase().includes(searchQuery.brand?.toLowerCase())
                && car.age.toString().includes(searchQuery.age);
          }
        case 3:
          return car.id.toString().includes(searchQuery.id)
              && car.brand?.toLowerCase().includes(searchQuery.brand?.toLowerCase())
              && car.age.toString().includes(searchQuery.age);
      }
    });
  })

</script>

<style lang="scss">
  .search-area {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 20px;
    margin: 20px 0;
  }
</style>
