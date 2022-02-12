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
  sprite: string
  constructor(name: string, honk: number, wingspan: number, neck: number, sprite: string) {
    this.name = name
    this.honk = honk
    this.wingspan = wingspan
    this.neck = neck
    this.sprite = sprite
  }
}
// breeds geese
  function breeder(firstGoose: Goose, secondGoose : Goose): Goose {
    return new Goose(childGooseHelperName(firstGoose, secondGoose),
    childGooseHelperHonk(firstGoose, secondGoose),
    childGooseHelperWingspan(firstGoose, secondGoose),
    childGooseHelperNeck(firstGoose, secondGoose))
  }  

// averages the honk stat vaule 
  function childGooseHelperHonk(firstGoose: Goose , secondGoose: Goose): number {
    return Math.round((firstGoose.honk + firstGoose.honk)/ 2) + (Math.floor(Math.random() * (10 - -10 )) + -10)
  }

// averages the wingspan stat value
  function childGooseHelperWingspan(firstGoose: Goose, secondGoose: Goose): number {
    return Math.round((firstGoose.wingspan + secondGoose.wingspan) / 2) + (Math.floor(Math.random() * (10 - -10 )) + -10)
  }

// averages the neck stat value
  function childGooseHelperNeck(firstGoose: Goose, secondGoose: Goose): number {
    return Math.round((firstGoose.wingspan + secondGoose.wingspan) / 2)  + (Math.floor(Math.random() * (10 - -10 )) + -10)
  }

 // STUB FIX NAME RANDOMIZER 
  function childGooseHelperName(firstGoose: Goose, secondGoose: Goose): string {
    return firstGoose.name
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
        new Goose('Huey', 50, 30, 10, "../assets/goosefinal.png")
      ]
    }
  }
}
</script>
