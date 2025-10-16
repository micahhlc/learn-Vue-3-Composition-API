<script setup>
  import { ref } from 'vue';

  const props = defineProps({
    details: {
      type: Array,
      required: false,
    },
  });
</script>
<template>
  <ul>
    <li v-for="detail in props.details">{{ detail }}</li>
  </ul>
</template>
