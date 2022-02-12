<template>
  <div class="home">
    <img alt="Mrs. Fens' Gaggle" src="../assets/logo.gif" style="height: 100%; display: inline-block; margin-bottom: 30px" /> 
    <main style="display: flex; flex-flow: row wrap; justify-content: center; gap: 20px;">
      <GooseComponent v-for="goose in geese" :key="goose.name" :name="goose.name" :honk="goose.honk" :wingspan="goose.wingspan" :neck="goose.neck"/>
    </main>
  </div>
</template>

<script lang="ts">
import GooseComponent from '@/components/Goose.vue';

class Goose {
  name: string
  honk: number
  wingspan: number
  neck: number
  constructor(name: string, honk: number, wingspan: number, neck: number) {
    this.name = name
    this.honk = honk
    this.wingspan = wingspan
    this.neck = neck
  }
}

class HatType {
  name: string
  image: string
  cute: number
  cool: number
  constructor(name: string, image: string, cute: number, cool: number) {
    this.name = name
    this.image = image
    this.cute = cute
    this.cool = cool
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
        new Goose('Huey', 50, 30, 10)
      ]
    }
  }
}
</script>
