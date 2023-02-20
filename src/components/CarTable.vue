<template>
  <table class="table table-striped table-bordered">
    <thead>
    <tr>
      <th
        v-for="heading in tableHeadings"
        :key="heading.id"
        scope="col"
        class="w-25"
        @click="setSort(heading)"
      >
        <div class="d-flex justify-content-between align-items-center" role="button">
          {{ heading.title }}
          <vertical-arrow :class="['sorting_arrow', { 'active-desc': heading.descSorting, 'active-esc': heading.escSorting } ]"/>
        </div>
      </th>
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
  import VerticalArrow from "@/components/iconComponents/VerticalArrow";
  import {reactive} from "vue";

  defineProps(['cars'])
  const emit = defineEmits(['sort-toggle'])

  const tableHeadings = reactive([
    {
      id: 1,
      title: 'ID',
      descSorting: false,
      escSorting: false
    },
    {
      id: 2,
      title: 'Brand',
      descSorting: false,
      escSorting: false
    },
    {
      id: 3,
      title: 'Year',
      descSorting: false,
      escSorting: false
    },
  ])

  const disableAllSorting = () => {
    tableHeadings.forEach(item => {
      item.descSorting = false
      item.escSorting = false
    })
  }

  function setSort(heading) {
    if (!heading.descSorting && !heading.escSorting)  {
      disableAllSorting()
      heading.descSorting = true
      emit('sort-toggle', '-' + heading.title?.toLowerCase())
    } else if (heading.descSorting) {
      heading.descSorting = false
      heading.escSorting = true
      emit('sort-toggle', heading.title?.toLowerCase())
    } else if (heading.escSorting) {
      disableAllSorting()
      emit('sort-toggle', '')
    }
  }
</script>

<style lang="scss" scoped>
  .sorting_arrow {
    opacity: 0;
    transition: all .2s ease;

    &.active-desc {
      opacity: 1;
    }
    &.active-esc {
      opacity: 1;
      transform: rotate(180deg);
    }
  }
</style>
