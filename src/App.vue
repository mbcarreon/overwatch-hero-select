<script setup>
import { ref, onMounted } from 'vue';
import heroesData from './heroes.json';

const heroes = ref(heroesData);
const currentHero = ref(0);
const videoRef = ref(null);
const currentAbility = ref(null);

const changeAbility = (abilityName) => {
  const selectedHero = heroes.value[currentHero.value];
  const selectedAbility = selectedHero.abilities.find(ability => ability.name === abilityName);
  currentAbility.value = { ...selectedAbility };
};

const changeHero = (id) => {
  currentHero.value = id - 1;
  videoRef.value?.load();
  changeAbility(heroes.value[currentHero.value].abilities[0].name);
};

onMounted(() => {
  changeAbility(heroes.value[currentHero.value].abilities[0].name);
});

const isAbilityActive = (abilityName) => {
  return currentAbility.value && currentAbility.value.name === abilityName;
};

const isHeroActive = (heroId) => {
  return currentHero.value === heroId;
};
</script>

<template>
  <div class="content">
    <div class="top-container">
      <h2>{{ heroes[currentHero].role }}</h2>
      <h1>{{ heroes[currentHero].name }}</h1>
      <div class="abilities">
        <div 
          v-for="ability in heroes[currentHero].abilities" 
          :key="ability.name" 
          @click="changeAbility(ability.name)"
          :class="{ 'active': isAbilityActive(ability.name) }"
        >
          <img :src="ability.icon">
        </div>
      </div>
      <h3 v-if="currentAbility">{{ currentAbility.name }}</h3>
      <h4 v-if="currentAbility">{{ currentAbility.description }}</h4>
    </div>
    <div class="bot-container">
      <div class="portraits">
        <div 
          class="corner-border" 
          v-for="(hero, index) in heroes"
          :key="hero.id" 
          @click="changeHero(hero.id)"
          :class="{ 'active': isHeroActive(index) }"
        >
            <img :src="hero.portrait">
        </div>
      </div>
      <button>Ready</button>
    </div>
    
    <video autoplay loop class="background" ref="videoRef">
      <source :src="heroes[currentHero].background" type="video/mp4">
    </video>
  </div>
</template>

<style scoped>
.content {
  width: 100%;
  height: 100vh;
  padding: 32px;
  display: flex;
  flex-direction: column;
}

.background {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  object-fit: cover;
  z-index: -1;
  transition: .5s;
}

.top-container {
  width: 100%;
  height: max-content;
  display: flex;
  flex-direction: column;
}

.bot-container {
  width: 100%;
  height: max-content;
  display: flex;
  flex-direction: column;
  gap: 24px;
  align-items: center;
  margin-top: auto;
}

h1,
h2,
h3,
h4 {
  margin: 0;
  text-shadow: 1px 1px 4px #060606;
}

h1 {
  color: rgb(93, 230, 247);
  font-family: 'DISPLAYEDOblique';
  font-weight: normal;
  font-style: normal;
  font-size: 8rem;
  letter-spacing: -18px;
  text-transform: uppercase;
  margin-bottom: -8px;
  margin-left: -13px;
}

h2 {
  font-family: 'DISPLAYEDOblique';
  font-weight: normal;
  font-style: normal;
  font-size: 1.8rem;
  letter-spacing: 2px;
  text-transform: uppercase;
  margin-bottom: -24px;
  margin-left: -2px;
}

h3 {
  font-family: 'DIN Next LT Pro';
  font-weight: 500;
  font-style: normal;
  font-size: 1.3rem;
  letter-spacing: 2px;
  text-transform: uppercase;
  margin-bottom: 2px;
}

h4 {
  width: 30%;
  font-family: 'DIN Next Rounded LT Pro';
  font-weight: 300;
  font-style: normal;
  font-size: .9rem;
}

.abilities {
  width: 20%;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  gap: 6px;
  margin-bottom: 16px;
}

.abilities div {
  width: 46px;
  height: 46px;
  padding: 10px;
  box-sizing: border-box;
  background-color: none;
  border-radius: 100%;
  background-color: rgba(255, 255, 255, 0.1);
  cursor: pointer;
}

.abilities div:hover,
.abilities .active {
  background-color: rgba(255, 255, 255, 0.4);
}

.portraits {
  width: 80%;
  height: max-content;
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
}

.portraits div {
  width: 50px;
  height: 50px;
  box-sizing: border-box;
  background-color: none;
  border: 1px solid rgba(255, 255, 255, 0.2);
  background-color: rgba(255, 255, 255, 0.2);
  backdrop-filter: blur(5px);
  cursor: pointer;
}

.portraits div:hover,
.portraits .active {
  border: 1px solid rgba(255, 255, 255, 1);
  background-color: rgba(255, 255, 255, 0.6);
}

.abilities img,
.portraits img {
  width: 100%;
  height: 100%;
  object-fit: contain;
}

.corner-border {
  --b: 1px;   /* thickness of the border */
  --c: rgb(255, 255, 255);   /* color of the border */
  --w: 1px;  /* width of border */
  
  border: var(--b) solid #0000; /* space for the border */
  --_g: #0000 90deg,var(--c) 0;
  --_p: var(--w) var(--w) border-box no-repeat;
  background:
    conic-gradient(from 90deg  at top    var(--b) left  var(--b),var(--_g)) 0    0    / var(--_p),
    conic-gradient(from 180deg at top    var(--b) right var(--b),var(--_g)) 100% 0    / var(--_p),
    conic-gradient(from 0deg   at bottom var(--b) left  var(--b),var(--_g)) 0    100% / var(--_p),
    conic-gradient(from -90deg at bottom var(--b) right var(--b),var(--_g)) 100% 100% / var(--_p);
}

button {
  width: max-content;
  padding: 8px 24px 5px 24px;
  box-shadow: 1px 1px 3px rgba(0, 0, 0, .5);
  border: none;
  background-color: rgb(240, 100, 20);
  color: #fff;
  font-family: 'DIN Next LT Pro';
  font-weight: 500;
  font-style: normal;
  font-size: 1.3rem;
  letter-spacing: 2px;
  text-transform: uppercase;
  text-shadow: 1px 1px 1px #757575;
  cursor: pointer;
}

button:hover {
  background-color: rgb(204, 87, 18);
}
</style>