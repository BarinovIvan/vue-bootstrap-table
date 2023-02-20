<template>
  <div class="container">
    <div class="search-area d-flex justify-content-center align-items-center gap-4 m-2">
      <div class="d-flex gap-4">
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
      </div>
      <div class="d-flex align-items-center gap-3">
        <p class="my-0 fw-bold">Select date range:</p>
        <CustomDatePicker
            title="Start:"
            @date-picked="setStartDate($event)"
        />
        <CustomDatePicker
            title="End:"
            @date-picked="setEndDate($event)"
        />
      </div>
    </div>
    <car-table :cars="filteredCarList" @sort-toggle="getCars($event)"/>
  </div>
</template>

<script setup>
import CarTable from "@/components/CarTable";
import CustomSearch from "@/components/ui/CustomSearch";
import {computed, reactive, ref} from "vue";
import CustomDatePicker from "@/components/ui/CustomDatePicker";
import axios from "axios";

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

  async function getCars(sort) {
    if (!sort) {
      console.log('https://localhost:3005/cars')
      await axios.get('https://localhost:3005/cars')
    } else {
      console.log('https://localhost:3005/cars/index?sort=' + sort)
      await axios.get('https://localhost:3005/cars/index?sort=' + sort)
    }
  }

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

  function setStartDate(date) {
    searchQuery.startDate = date
  }
  function setEndDate(date) {
    searchQuery.endDate = date
  }

  function isCarAgeInDateRange(car) {
  if (searchQuery.startDate && searchQuery.endDate) {
    return car.age >= searchQuery.startDate && car.age <= searchQuery.endDate
  } else return true
}

  const filteredCarList = computed(() => {
    return cars.filter(car => {
      if (searchQuery.id) {
        if (searchQuery.brand) {
          return car.id.toString().includes(searchQuery.id)
              && car.brand?.toLowerCase().includes(searchQuery.brand?.toLowerCase())
              && isCarAgeInDateRange(car)
        } else {
          return car.id.toString().includes(searchQuery.id) && isCarAgeInDateRange(car)
        }
      } else if (searchQuery.brand) {
        return car.brand?.toLowerCase().includes(searchQuery.brand?.toLowerCase()) && isCarAgeInDateRange(car)
      } else {
        return isCarAgeInDateRange(car)
      }
    });
  })
</script>

<style lang="scss" scoped>
  .search-area {
    @media (max-width: 1024px) {
      flex-wrap: wrap;
    }
  }
</style>
