<template>
  <h4>Your Balence</h4>
  <h1 id="balence">{{total}}</h1>
</template>

<script setup>

import  {defineProps} from 'vue';

const props = defineProps({
  total: {
    type: Number,
    required: true,
  }
})

</script>
