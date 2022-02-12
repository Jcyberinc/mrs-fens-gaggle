<template>
  <div class="home">
    <img alt="Mrs. Fens' Gaggle" src="../assets/logo.gif" style="height: 100%; display: inline-block; margin-bottom: 30px" /> 
    <main style="display: flex; flex-flow: row wrap; justify-content: center; gap: 20px;">
      <GooseComponent v-for="goose in geese" :key="goose.name" :name="goose.name" :honk="goose.honk"
      :wingspan="goose.wingspan" :neck="goose.neck" :sprite="goose.sprite"/>
    </main>
  </div>
</template>

<script lang="ts">
import GooseComponent from '@/components/Goose.vue';
import Vue from 'vue';

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

  leave(geese: Goose[]) {
    geese.splice(geese.indexOf(this), 1);
  }
}
// breeds geese
  function breeder(firstGoose: Goose, secondGoose : Goose, sprite: string): Goose {
    return new Goose(childGooseHelperName(firstGoose, secondGoose),
    childGooseHelperHonk(firstGoose, secondGoose),
    childGooseHelperWingspan(firstGoose, secondGoose),
    childGooseHelperNeck(firstGoose, secondGoose),
    sprite)
  }  

// averages the honk stat vaule 
function childGooseHelperHonk(firstGoose: Goose , secondGoose: Goose): number {
  return Math.round((firstGoose.honk + firstGoose.honk)/ 2) + (Math.floor(Math.random() * (11 - -10)) + -10)
}

// averages the wingspan stat value
function childGooseHelperWingspan(firstGoose: Goose, secondGoose: Goose): number {
  return Math.round((firstGoose.wingspan + secondGoose.wingspan) / 2) + (Math.floor(Math.random() * (11 - -10)) + -10)
}

// averages the neck stat value
function childGooseHelperNeck(firstGoose: Goose, secondGoose: Goose): number {
  return Math.round((firstGoose.wingspan + secondGoose.wingspan) / 2)  + (Math.floor(Math.random() * (11 - -10)) + -10)
}

 // STUB FIX NAME RANDOMIZER 
function childGooseHelperName(firstGoose: Goose, secondGoose: Goose): string {
  return firstGoose.name
} 

// random stat generator for the spawning geese
function randomStatGen(): Goose {
  return new Goose("StubNameGen", randomNum(), randomNum(), randomNum(), "no hat" )
}

// creates the random number 
function randomNum(): number {
  return Math.random() * 101 
}

// name generator





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

export default Vue.extend({
  name: 'Home',
  components: {
    GooseComponent
  },
  data: function() {
    return {
      geese: [
        new Goose('Huey', 50, 30, 10, require("@/assets/goosefinal.png"))
      ],
      hats: [
        new HatType('No Hat', "/@/assets/goosefinal.png", 0, 0),
        new HatType('Propeller', "/@/assets/goosepropellor.png", 7, -2),
        new HatType('Top Hat', "/@/assets/goosetophat.png", -3, 8),
        new HatType('Bearskin', "/@/assets/goosebearskin.png", -5, 10),
        new HatType('Party Hat', "/@/assets/partygoose.png", 6, -1),
        new HatType('Crown', "/@/assets/kinggoose.png", -2, 7),
        new HatType('Bonnet', "/@/assets/babygoose.png", 9, -4),
        new HatType('Santa', "/@/assets/santagoose.png", 6, -1),
        new HatType('Chefs Hat', "/@/assets/chefgoose.png", 1, 4),
        new HatType('Frog Hat', "/@/assets/chefgoose.png", 10, -5),
        new HatType('Rotten Banana', "/@/assets/bananagoose.png", -10, -10)
      ]
    }
  },
  methods: {
    spawnGoose() {
      window.setTimeout(this.spawnGoose, 60_000);
      let goose = new Goose('Goose', 50, 30, 10, require("@/assets/goosefinal.png"));
      window.setTimeout(() => goose.leave(this.geese), 210_000)
      this.geese.push(goose);
    }
  },
  mounted () {
    window.setTimeout(this.spawnGoose, 30_000);
  }
});
</script>
