<template>
  <div class="date-picker">
    <label>{{ title }}</label>
    <input
        v-model="date"
        type="number"
        min="1900"
        max="2099"
        step="1"
        class="form-control w-100"
        @change="emits('date-picked', date)"
    />
  </div>
</template>

<script setup>
  import {ref} from "vue";

  defineProps(['title'])
  const emits = defineEmits(['date-picked'])

  let date = ref(null)
</script>
