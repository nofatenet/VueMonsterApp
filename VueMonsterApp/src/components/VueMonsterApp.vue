<template>
  <div>
    <p>{{ playerHealth }}</p>

    <section class="row dust">
      <div class="small-6 columns">
        <h1 class="text-center">Our Hero</h1>
        <img src="ourHero.png" alt="ourHero" v-if="playerHealth > 0 && !playerAttack" />
        <img src="ourHeroWon.png" alt="ourHeroWon" v-else-if="playerHealth > 0 && playerWon" />
        <img
          src="ourHeroAttackAnimation1.gif"
          alt="ourHeroAttack"
          v-else-if="playerHealth > 0 && playerAttack && !playerWon"
        />
        <img src="ourHeroDead.png" alt="ourHeroDead" v-else-if="playerHealth < 0" />
        <div class="healthbar">
          <div
            class="healthbar text-center"
            style="background-color: green;
                    margin: 0; color: #ccc;"
            :style="{ width: playerHealth + '%'}"
          >{{ playerHealth }}</div>
          <p class="info">Special Attacks left: {{ playerSpecials }}</p>
          <p class="info">Heal Packs left: {{ playerHeals }}</p>
        </div>
      </div>
      <div class="small-6 columns">
        <h1 class="text-center">The Monster</h1>
        <img src="theMonster.png" alt="theMonster" v-if="monsterHealth > 0" />
        <img src="theMonsterDead.png" alt="theMonsterDead" v-else />
        <div class="healthbar">
          <div
            class="healthbar text-center"
            style="background-color: green; margin: 0;
                    color: #ccc;"
            :style="{ width: monsterHealth + '%'}"
          >{{ monsterHealth }}</div>
        </div>
      </div>
    </section>
    <section class="row controls" v-if="!gameIsRunning">
      <div class="small-12 columns">
        <button id="start-game" v-on:click="startGame">START NEW GAME</button>
      </div>
    </section>
    <section class="row controls" v-else>
      <div class="small-12 columns">
        <button id="attack" @click="attack">ATTACK</button>
        <button id="special-attack" @click="specialAttack">SPECIAL ATTACK</button>
        <button id="heal" @click="heal">HEAL</button>
        <button id="give-up" @click="giveUp">GIVE UP</button>
      </div>
    </section>
    <section class="row log">
      <div class="small-12 columns">
        <ul>
          <li></li>
        </ul>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  components: {},
  data() {
    return {
      playerHealth: 100,
      monsterHealth: 100,
      gameIsRunning: false,
      playerAttack: false,
      playerWon: false,
      playerSpecials: 1,
      playerHeals: 3,
      testWert: 3
    };
  },
  methods: {
    startGame: function() {
      this.gameIsRunning = true;
      this.playerHealth = 100;
      this.monsterHealth = 100;
    },
    attack: function() {
      // Hero Attacks:
      let damage = this.calcDmg(3, 12);
      this.monsterHealth -= damage;
      this.playerAttack = true;

      setTimeout(() => {
        this.playerAttack = false;
      }, 2000);

      if (this.monsterHealth <= 0) {
        alert("Hero won!");

        this.playerAttack = false;
        this.playerWon = true;

        this.gameInRunning = false;
        return; //Exit function if Monster is dead.
      }

      // Monster Attacks:
      damage = this.calcDmg(4, 13);
      this.playerHealth -= damage;

      if (this.playerHealth <= 0) {
        alert("Hero is lost!");
        this.gameInRunning = false;
      }
    },
    specialAttack: function() {
      // Hero Special Attack:
      if (this.playerSpecials > 0) {
        let damage = this.calcDmg(13, 33);
        this.monsterHealth -= damage;
        //this.playerSpecialAttack = true;
        this.playerSpecials--;
      } else {
        alert("Out of Specials! No Damage was dealt to the Monster!");
      }

      // Monster Attacks:
      if (this.monsterHealth > 0) {
        this.damage = this.calcDmg(4, 11);
        this.playerHealth -= this.damage;
        return;
      }
    },
    heal: function() {
      // Hero Special Attack:
      if (this.playerHeals > 0 && this.playerHealth < 100) {
        this.playerHealth += 9;
        //this.playerHeals = true;
        this.playerHeals--;
      } else if (this.playerHeals > 0) {
        alert("No can do! Health is at max!");
      } else {
        alert("Out of Heal Packs! No healing recieved!");
      }

      // Monster Attacks:
      if (this.monsterHealth > 0) {
        this.damage = this.calcDmg(4, 11);
        this.playerHealth -= this.damage;
        return;
      }
    },
    giveUp: function() {},
    calcDmg: function(min, max) {
      return Math.max(Math.floor(Math.random() * max) + 1, min);
    }
  },
  created() {}
};
</script>

<style scoped>
@import "./assets/foundation.min.css";

body {
  background-color: #000;
  color: #999;
}
img {
  text-align: center;
  margin-left: 200px;
  margin-bottom: 24px;
  transform: scale(2);
  image-rendering: crisp-edges;
}

p {
  margin: auto;
}

.info {
  font-size: smaller;
}

.row.dust {
  background-image: linear-gradient(
    to top,
    rgba(200, 102, 140, 0.2),
    rgba(11, 11, 111, 0)
  );
}

.text-center {
  text-align: center;
}

.healthbar {
  width: 80%;
  height: 20px;
  background-color: #333;
  margin: auto;
  margin-bottom: 10px;
  transition: width 500ms;
  border-radius: 3px;
}

.controls,
.log {
  margin-top: 30px;
  text-align: center;
  padding: 2px;
  border: 1px solid #ccc;
  box-shadow: 0px 3px 6px #ccc;
}

.turn {
  margin-top: 20px;
  margin-bottom: 20px;
  font-weight: bold;
  font-size: 22px;
}

.log ul {
  list-style: none;
  font-weight: bold;
  text-transform: uppercase;
}

.log ul li {
  margin: 5px;
}

.log ul .player-turn {
  color: blue;
  background-color: #e4e8ff;
}

.log ul .monster-turn {
  color: red;
  background-color: #ffc0c1;
}

button {
  font-size: 20px;
  background-color: #eee;
  padding: 12px;
  box-shadow: 0 1px 1px black;
  margin: 10px;
  color: #333;
}

#start-game {
  background-color: #aaffb0;
}

#start-game:hover {
  background-color: #76ff7e;
}

#attack {
  background-color: #ff7367;
}

#attack:hover {
  background-color: #ff3f43;
}

#special-attack {
  background-color: #ffaf4f;
}

#special-attack:hover {
  background-color: #ff9a2b;
}

#heal {
  background-color: #aaffb0;
}

#heal:hover {
  background-color: #76ff7e;
}

#give-up {
  background-color: #ffffff;
}

#give-up:hover {
  background-color: #c7c7c7;
}
</style>