<template>
  <div>
    <h1>Breeding</h1>
      <table>
        <tr>
        <td> <button v-for="goose in geese" :key="goose.name"> {{goose.name}} </button>
        </td>
      </tr>
      </table>
  </div>
</template>

<script lang="ts">
export default {
  props: {
    geese: Array
  }
};
</script>