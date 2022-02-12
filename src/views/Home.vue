<template>
  <div class="home">
    <img alt="Mrs. Fens' Gaggle" src="../assets/logo.gif" style="height: 100%; display: inline-block; margin-bottom: 30px" /> 
    <main style="display: flex; flex-flow: row wrap; justify-content: center; gap: 20px;">
      <GooseComponent v-for="goose in geese" :key="goose.name" :name="goose.name" />
    </main>
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

class HatType {

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
        new Goose('Louie'),
        new Goose('Donald'),
        new Goose('Goose'),
        new Goose('Scrooge'),
        new Goose('Duck'),
        new Goose('Daffy'),
        new Goose('Bugs'),
        new Goose('Porky'),
        new Goose('Taz'),
      ]
    }
  }
}
</script>
