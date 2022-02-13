<template>
  <div class="home">
    <img
      alt="Ms. Fen's Gaggle"
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
        :fertile="goose.fertility"
        :selected="goose.selected"
        :sprite="goose.sprite"
        @click.native="addToBreedQueue(goose)"
      />
    </main>
    <div
      v-if="rating"
      style="
        position: fixed;
        left: 0;
        right: 0;
        top: 0;
        bottom: 0;
        background-color: rgb(0, 0, 0, 0.4);
        display: flex;
      "
    >
      <img
        src="@/assets/MRSFENS.png"
        style="
          position: absolute;
          left: 0px;
          bottom: 0;
          width: 400px;
          height: 400px;
        "
      />
      <div
        style="
          margin: auto;
          width: 500px;
          padding: 20px;
          border-radius: 20px;
          background-color: rgb(255, 255, 255);
          z-index: 1000;
        "
      >
        <p v-if="maxGoose <= 0">Looks like ya didn't bring me a goose!</p>
        <p v-if="maxGoose > 0 && maxGoose <= 20">
          Ya sure that’s a goose you brought me there? Cause they look more like
          an odd duck than a goose! Try again. I’m sure
          you can do much better than that. Told ya this is tough work. If ya
          can’t handle it you should go breed ducks. It seems you’re a natural
          at it!
        </p>
        <p v-if="maxGoose > 20 && maxGoose <= 40">
          Hm… still debatable whether this little fella here is a goose, but
          after all the geese you’ve shown me before it could be worse. Ay don’t
          gimme that look! You’re improvin’, slowly but surely.
          Just keep workin’ on yer skills and I’m sure you’ll create a mighty
          fine goose! Even if it’ll probably take ya a couple years longer than
          usual…
        </p>
        <p v-if="maxGoose > 40 && maxGoose <= 60">
          Eh… that’s a goose alright but they’re just that y’know? Don’t have
          that little spark in their eyes, a beginnin’ of something special,
          something that would truly make them an impeccable little fella. A
          shame but what can ya do? Most geese I’ve seen in ma life have been like this one so I wouldn’t be ashamed.
        </p>
        <p v-if="maxGoose > 60 && maxGoose <= 80">
          You’re gettin’ there with that goose over there! Just
          gotta keep at it for a bit longer. Haha! Ya sure are learnin’ faster
          than I thought. I’d never thought in ma life that someone like you
          could get this close to the levels of a professional like me, yet here
          ya are.
        </p>
        <p v-if="maxGoose > 80 && maxGoose <= 90">
          Ooo… you’re gettin’ so close! I could feel it in ma
          bones. Just trust me on this one, I have years of experience to
          back it up. I’m sure you’ll get the goose of your dreams soon if you
          keep at it!
        </p>
        <p v-if="maxGoose > 90 && maxGoose <= 95">
          Oh my! Ain’t that a mighty fine goose ya got there! Just look at em!
          They’re pretty as a peach and just so polite, with a glimmer of
          something special in those eyes. See? I told ya you would succeed if
          ya worked hard enough. Look at how far you’ve come! Now
          I’ve seen geese better than this one, but that might be difficult even
          for you.
        </p>
        <p v-if="maxGoose > 95 && maxGoose <= 99">
          WOWZERS! I shoulda seen this one comin’ but you’ve exceeded all ma
          expectations. I’ve only seen a few geese in ma life as
          amazin’ as this one. And trust me I’ve seen plenty of geese, probably
          more than a sane person should. Could there be a better
          goose out there? I’m not sure if it’s even possible but hm…
        </p>
        <p v-if="maxGoose > 99">
          Oh. My. Heavens! I… I can’t believe it! I never
          thought I would see a goose as perfectly holy and divine as this
          one. Yet here’s one right before me. If there’s a god of geese out
          there I bet ma money that this one here would lead them all. Words
          can’t describe how proud I am of you. I deem this goose a Zoose out of
          100.
        </p>
      </div>
    </div>
    <img
      src="@/assets/rate.png"
      height="100px"
      width="100px"
      @click="
        rating = !rating;
        maxGoose = maxGooser();
      "
      style="position: absolute; top: 20px; left: 20px"
    />
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
  selected: boolean;
  constructor(
    name: string,
    honk: number,
    wingspan: number,
    neck: number,
    cute: number,
    cool: number,
    sprite: string,
    hatID: number,
    fertility: boolean,
    selected: boolean
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
    this.selected = selected;
  }

  leave(geese: Goose[]) {
    geese.splice(geese.indexOf(this), 1);
  }

  changeFert(fert: boolean) {
    this.fertility = fert;
  }

  select() {
    this.selected = !this.selected;
  }
}

// averages the honk stat vaule
function childGooseHelperHonk(firstGoose: Goose, secondGoose: Goose): number {
  return (
    Math.round((firstGoose.honk + firstGoose.honk) / 2) +
    (Math.floor(Math.random() * (16 - -15)) + -15)
  );
}

// averages the wingspan stat value
function childGooseHelperWingspan(
  firstGoose: Goose,
  secondGoose: Goose
): number {
  return (
    Math.round((firstGoose.wingspan + secondGoose.wingspan) / 2) +
    (Math.floor(Math.random() * (16 - -15)) + -15)
  );
}

// averages the neck stat value
function childGooseHelperNeck(firstGoose: Goose, secondGoose: Goose): number {
  return (
    Math.round((firstGoose.neck + secondGoose.neck) / 2) +
    (Math.floor(Math.random() * (16 - -15)) + -15)
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
        true,
        false
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
      let goose = new Goose(
        randomName(),
        childGooseHelperHonk(firstGoose, secondGoose),
        childGooseHelperWingspan(firstGoose, secondGoose),
        childGooseHelperNeck(firstGoose, secondGoose),
        hat.cute,
        hat.cool,
        hat.image,
        hat.id,
        true,
        false
      );
      window.setTimeout(() => goose.leave(this.geese), 210_000);
      this.geese.push(goose);
    },
    addToBreedQueue(goose: Goose) {
      if (this.breedQueue.length == 0) {
        goose.select();
        this.breedQueue.push(goose);
      } else if (this.breedQueue.length == 1) {
        let gander = this.breedQueue[0];
        if (goose != gander) {
          if (goose.fertility == true && gander.fertility == true) {
            gander.select();
            this.breeder(goose, gander, this.hats[0].image);
            goose.changeFert(false);
            gander.changeFert(false);
            window.setTimeout(() => goose.changeFert(true), 60_000);
            window.setTimeout(() => gander.changeFert(true), 60_000);
            this.breedQueue.splice(0);
          } else {
            gander.select();
            this.breedQueue.splice(0);
          }
        } else {
          this.breedQueue.splice(0);
          goose.select();
        }
      }
    },
    maxGooser(): number {
      if (this.breedQueue.length == 0) {
        return 0;
      } else {
        let gander = this.breedQueue[0];
        gander.select();
        this.breedQueue.splice(0);
        return Math.max(gander.cute, gander.cool) / 4;
      }
    },
  },
  data: function () {
    return {
      maxGoose: Number,
      rating: false,
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
      true,
      false
    );
    window.setTimeout(() => huey.leave(this.geese), 210_000);
    this.geese.push(huey);
  },
});
</script>
