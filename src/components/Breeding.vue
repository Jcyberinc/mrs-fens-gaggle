<template>
<div>
    <h1>Breeding</h1>
    <button v-for="goose in geese" :key="goose.name"> {{goose.name}} </button>
</div>
</template>

<script lang="ts">
export default {
  props: {
    geese: Array
  }
};
</script>