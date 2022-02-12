<template>
  <div class="home">
    <img
      alt="Ms. Fens' Gaggle"
      src="@/assets/logofinal.png"
      style="display: inline-block; margin-bottom: 60px"
    />

    <main
      style="
        display: flex;
        flex-flow: row wrap;
        justify-content: center;
        gap: 40px;
      "
    >
      <GooseComponent
        v-for="goose in geese"
        :key="goose.name"
        :name="goose.name"
        :honk="goose.honk"
        :wingspan="goose.wingspan"
        :neck="goose.neck"
        :cute="goose.cute"
        :cool="goose.cool"
        :sprite="goose.sprite"
        @click.native="addToBreedQueue(goose)"
      />
    </main>
  </div>
</template>

<script lang="ts">
import GooseComponent from "@/components/Goose.vue";
import { array as ManyNames } from "@/assets/names.json";
import Vue from "vue";

class Goose {
  name: string;
  honk: number;
  wingspan: number;
  neck: number;
  cute: number;
  cool: number;
  sprite: string;
  hatID: number;
  fertility: boolean;
  constructor(
    name: string,
    honk: number,
    wingspan: number,
    neck: number,
    cute: number,
    cool: number,
    sprite: string,
    hatID: number,
    fertility: boolean
  ) {
    this.name = name;
    this.honk = honk;
    this.wingspan = wingspan;
    this.neck = neck;
    this.cute = 100 - honk + (100 - wingspan) + (100 - neck) + cute * 10;
    if (neck > 75) {
      this.cool = honk + wingspan + cool * 10 - 50;
    } else {
      this.cool = honk + wingspan + neck + cool * 10;
    }
    this.sprite = sprite;
    this.hatID = hatID;
    this.fertility = fertility;
  }

  leave(geese: Goose[]) {
    geese.splice(geese.indexOf(this), 1);
  }

  changeFert(geese: Goose[], fert: boolean) {
    geese.splice(geese.indexOf(this), 1);
    geese.push(
      new Goose(
        this.name,
        this.honk,
        this.wingspan,
        this.neck,
        this.cute,
        this.cool,
        this.sprite,
        this.hatID,
        fert
      )
    );
  }
}

// averages the honk stat vaule
function childGooseHelperHonk(firstGoose: Goose, secondGoose: Goose): number {
  return (
    Math.round((firstGoose.honk + firstGoose.honk) / 2) +
    (Math.floor(Math.random() * (11 - -10)) + -10)
  );
}

// averages the wingspan stat value
function childGooseHelperWingspan(
  firstGoose: Goose,
  secondGoose: Goose
): number {
  return (
    Math.round((firstGoose.wingspan + secondGoose.wingspan) / 2) +
    (Math.floor(Math.random() * (11 - -10)) + -10)
  );
}

// averages the neck stat value
function childGooseHelperNeck(firstGoose: Goose, secondGoose: Goose): number {
  return (
    Math.round((firstGoose.neck + secondGoose.neck) / 2) +
    (Math.floor(Math.random() * (11 - -10)) + -10)
  );
}

// STUB FIX NAME RANDOMIZER
function childGooseHelperName(firstGoose: Goose, secondGoose: Goose): string {
  return firstGoose.name;
}

// creates the random number
function randomNum(): number {
  return Math.floor(Math.random() * 101);
}

// name generator
function randomName(): string {
  return ManyNames[Math.floor(Math.random() * ManyNames.length)];
}

class HatType {
  id: number;
  name: string;
  image: string;
  cute: number;
  cool: number;
  constructor(
    id: number,
    name: string,
    image: string,
    cute: number,
    cool: number
  ) {
    this.id = id;
    this.name = name;
    this.image = image;
    this.cute = cute;
    this.cool = cool;
  }
}

export default Vue.extend({
  name: "Home",
  components: {
    GooseComponent,
  },
  methods: {
    spawnGoose() {
      window.setTimeout(this.spawnGoose, 60_000);
      let goose = this.randomStatGen();
      window.setTimeout(() => goose.leave(this.geese), 210_000);
      this.geese.push(goose);
    },
    // random stat generator for the spawning geese
    randomStatGen(): Goose {
      let hat = this.randomHat();
      return new Goose(
        randomName(),
        randomNum(),
        randomNum(),
        randomNum(),
        hat.cute,
        hat.cool,
        hat.image,
        hat.id,
        true
      );
    },
    randomHat(): HatType {
      if (Math.random() < 0.001) return this.banana;
      if (Math.random() < 0.1)
        return this.hats[Math.floor(Math.random() * this.hats.length)];
      else return this.hats[0];
    },
    childGooseHelperHat(firstGoose: Goose, secondGoose: Goose): HatType {
      if (
        firstGoose.sprite != require("@/assets/goosefinal.png") ||
        secondGoose.sprite != require("@/assets/goosefinal.png")
      ) {
        return this.hats[
          Math.random() < 0.5 ? firstGoose.hatID : secondGoose.hatID
        ];
      } else {
        return this.hats[0];
      }
    },
    breeder(firstGoose: Goose, secondGoose: Goose, sprite: string) {
      let hat = this.childGooseHelperHat(firstGoose, secondGoose);
      this.geese.push(
        new Goose(
          randomName(),
          childGooseHelperHonk(firstGoose, secondGoose),
          childGooseHelperWingspan(firstGoose, secondGoose),
          childGooseHelperNeck(firstGoose, secondGoose),
          hat.cute, //PLACEHOLDER CODE UNTIL ACTUAL HELPERS MADE
          hat.cool, //PLACEHOLDER CODE UNTIL ACTUAL HELPERS MADE
          hat.image,
          hat.id,
          true
        )
      );
    },
    addToBreedQueue(goose: Goose) {
      if (this.breedQueue.length == 0) {
        this.breedQueue.push(goose);
      } else if (this.breedQueue.length == 1) {
        if (goose != this.breedQueue[0]) {
          if (goose.fertility == true && this.breedQueue[0].fertility == true) {
            this.breeder(goose, this.breedQueue[0], this.hats[0].image);
            goose.changeFert(this.geese, false);
            this.breedQueue[0].changeFert(this.geese, false);
            window.setTimeout(() => goose.changeFert(this.geese, true), 60_000);
            window.setTimeout(
              () => this.breedQueue[0].changeFert(this.geese, true),
              60_000
            );
            this.breedQueue.splice(0);
          } else {
            this.breedQueue.splice(0);
          }
        }
      }
    },
  },
  data: function () {
    return {
      geese: Array<Goose>(),
      breedQueue: Array<Goose>(),
      hats: [
        new HatType(0, "No Hat", require("@/assets/goosefinal.png"), 0, 0),
        new HatType(
          1,
          "Propeller",
          require("@/assets/goosepropellor.png"),
          7,
          -2
        ),
        new HatType(2, "Top Hat", require("@/assets/goosetophat.png"), -3, 8),
        new HatType(
          3,
          "Bearskin",
          require("@/assets/goosebearskin.png"),
          -5,
          10
        ),
        new HatType(4, "Party Hat", require("@/assets/partygoose.png"), 6, -1),
        new HatType(5, "Crown", require("@/assets/kinggoose.png"), -2, 7),
        new HatType(6, "Bonnet", require("@/assets/babygoose.png"), 9, -4),
        new HatType(7, "Santa", require("@/assets/santagoose.png"), 6, -1),
        new HatType(8, "Chefs Hat", require("@/assets/chefgoose.png"), 1, 4),
        new HatType(9, "Frog Hat", require("@/assets/goosefroggy.png"), 10, -5),
      ],
      banana: new HatType(
        10,
        "Rotten Banana",
        require("@/assets/bannanahosk.png"),
        -10,
        -10
      ),
    };
  },
  mounted() {
    window.setTimeout(this.spawnGoose, 3_000);
    let huey = new Goose(
      "Huey",
      50,
      30,
      10,
      0,
      0,
      require("@/assets/goosefinal.png"),
      0,
      true
    );
    window.setTimeout(() => huey.leave(this.geese), 18_000);
    this.geese.push(huey);
  },
});
</script>
