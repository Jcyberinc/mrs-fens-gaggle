<template>
  <div class="home">
    <img alt="Mrs. Fens' Gaggle" src="@/assets/logo.png" style="display: inline-block; transform: scale(0.5); margin-bottom: 30px;" /> 
    <main style="display: flex; flex-flow: row wrap; justify-content: center; gap: 20px;">
      <GooseComponent v-for="goose in geese" :key="goose.name" :name="goose.name" :honk="goose.honk"
      :wingspan="goose.wingspan" :neck="goose.neck" :cute="goose.cute" :cool="goose.cool" :sprite="goose.sprite"/>
    </main>
  </div>
</template>

<script lang="ts">
import GooseComponent from '@/components/Goose.vue';
import { array as ManyNames } from '@/assets/names.json'; 
import Vue from 'vue';

class Goose {
  name: string
  honk: number
  wingspan: number
  neck: number
  cute: number
  cool: number
  sprite: string
  constructor(name: string, honk: number, wingspan: number, neck: number, cute: number, cool: number, sprite: string) {
    this.name = name
    this.honk = honk
    this.wingspan = wingspan
    this.neck = neck
    this.cute = (100-honk) + (100-wingspan) + (100-neck) + cute
    if(neck>75){
      this.cool = honk + wingspan + cool - 100
    } else {
      this.cool = honk + wingspan + neck + cool
    }
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
    randomNum(), //PLACEHOLDER CODE UNTIL ACTUAL HELPERS MADE
    randomNum(), //PLACEHOLDER CODE UNTIL ACTUAL HELPERS MADE
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



// creates the random number 
function randomNum(): number {
  return Math.floor(Math.random() * 101);
}

// name generator
function randomName(): string {

  return ManyNames[Math.floor(Math.random() * ManyNames.length)]
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

export default Vue.extend({
  name: 'Home',
  components: {
    GooseComponent
  },
  methods: {
    spawnGoose() {
      window.setTimeout(this.spawnGoose, 6_000);
      let goose = this.randomStatGen();
      window.setTimeout(() => goose.leave(this.geese), 21_000)
      this.geese.push(goose);
    },
    // random stat generator for the spawning geese
    randomStatGen(): Goose {
      let hat = this.randomHat();
      return new Goose(randomName(), randomNum(), randomNum(), randomNum(), hat.cute, hat.cool, hat.image)
    },
    randomHat(): HatType {
      if (Math.random() < 0.1) return this.hats[Math.floor(Math.random() * this.hats.length)];
      else return this.hats[0];
    }
  },
  data: function() {
    return {
      geese: [
        new Goose('Huey', 50, 30, 10, 0, 0, require("@/assets/goosefinal.png"))
      ],
      hats: [
        new HatType('No Hat', require("@/assets/goosefinal.png"), 0, 0),
        new HatType('Propeller', require("@/assets/goosepropellor.png"), 7, -2),
        new HatType('Top Hat', require("@/assets/goosetophat.png"), -3, 8),
        new HatType('Bearskin', require("@/assets/goosebearskin.png"), -5, 10),
        new HatType('Party Hat', require("@/assets/partygoose.png"), 6, -1),
        new HatType('Crown', require("@/assets/kinggoose.png"), -2, 7),
        new HatType('Bonnet', require("@/assets/babygoose.png"), 9, -4),
        new HatType('Santa', require("@/assets/santagoose.png"), 6, -1),
        new HatType('Chefs Hat', require("@/assets/chefgoose.png"), 1, 4),
        new HatType('Frog Hat', require("@/assets/chefgoose.png"), 10, -5),
        new HatType('Rotten Banana', require("@/assets/banangoose.png"), -10, -10)
      ]
    }
  },
  mounted () {
    window.setTimeout(this.spawnGoose, 3_000);
  }
});
</script>
