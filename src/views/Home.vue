<template>
  <div class="home">
    <h1>Mrs. Fens' Gaggle</h1>
    <GooseComponent v-for="goose in geese" :key="goose.name" :name="goose.name" style="padding:10px" />
  </div>
</template>

<script lang="ts">
import GooseComponent from '@/components/Goose.vue';

class Goose {
  name: string
  constructor(name: string) {
    this.name = name
  }
}

export default {
  name: 'Home',
  components: {
    GooseComponent
  },
  data: function() {
    return {
      geese: [
        new Goose('Huey'),
        new Goose('Dewey'),
        new Goose('Louie')
      ]
    }
  }
}
</script>
