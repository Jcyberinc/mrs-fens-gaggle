<template>
  <div>
    <table>
        <tr>
        <td> &nbsp;Breeding
        </td>
        </tr>
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