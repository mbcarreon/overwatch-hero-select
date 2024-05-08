<script setup>
import { ref, computed, onMounted } from 'vue';
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
  heroId -= 1;
  return currentHero.value === heroId;
};

const tankHeroes = computed(() => heroes.value.filter(hero => hero.role === 'Tank'));
const damageHeroes = computed(() => heroes.value.filter(hero => hero.role === 'Damage'));
const supportHeroes = computed(() => heroes.value.filter(hero => hero.role === 'Support'));
</script>

<template>
  <div class="content">
    <div class="top-container">
      <div class="left-container flex-start">
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
      <div class="right-container flex-end">
        <div class="selected-hero">
          <div></div>
          <div></div>
          <div></div>
          <div></div>
          <div></div>
        </div>
      </div>
    </div>
    <div class="bottom-container" >
      <div class="portraits-container">
        <div class="portraits">
          <div 
            v-for="(hero, index) in tankHeroes"
            :key="hero.id" 
            @click="changeHero(hero.id)"
            :class="{ 'active': isHeroActive(hero.id) }"
          >
              <img :src="hero.portrait">
          </div>
        </div>
        <div class="portraits">
          <div 
            v-for="(hero, index) in damageHeroes"
            :key="hero.id" 
            @click="changeHero(hero.id)"
            :class="{ 'active': isHeroActive(hero.id) }"
          >
              <img :src="hero.portrait">
          </div>
        </div>
        <div class="portraits">
          <div 
            v-for="(hero, index) in supportHeroes"
            :key="hero.id" 
            @click="changeHero(hero.id)"
            :class="{ 'active': isHeroActive(hero.id) }"
          >
              <img :src="hero.portrait">
          </div>
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
  flex-direction: row;
}

.left-container,
.right-container {
  width: 50%;
  display: flex;
  flex-direction: column;
}

.flex-start {
  align-items: flex-start;
}

.flex-end {
  align-items: flex-end;
}

.bottom-container {
  width: 100%;
  height: max-content;
  display: flex;
  flex-direction: column;
  gap: 16px;
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
  width: 50%;
  font-family: 'DIN Next Rounded LT Pro';
  font-weight: 300;
  font-style: normal;
  font-size: .9rem;
}

.abilities {
  width: 50%;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  gap: 6px;
  margin-bottom: 16px;
}

.abilities div {
  width: 45px;
  height: 45px;
  padding: 10px;
  box-sizing: border-box;
  background-color: none;
  border-radius: 100%;
  background-color: rgba(0, 0, 0, 0.2);
  cursor: pointer;
  transition: .2s;
}

.abilities div:hover,
.abilities .active {
  background-color: rgba(0, 0, 0, 0.6);
}

.portraits-container {
  width: 90%;
  display: flex;
  flex-direction: row;
  gap: 16px;
  align-items: center;
  align-content: center;
}

.portraits-container > .portraits {
  flex: 1;
}

.portraits-container > .portraits:nth-child(2) {
  flex: 1.5;
}

.portraits {
  height: max-content;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  align-items: center;
  gap: 4px;
}

.portraits div {
  width: 45px;
  height: 45px;
  box-sizing: border-box;
  background-color: none;
  border-radius: 4px;
  border: 1px solid rgba(255, 255, 255, 0.2);
  background-color: rgba(0, 0, 0, 0.4);
  backdrop-filter: blur(5px);
  cursor: pointer;
  transition: .2s;
}

.portraits div:hover {
  z-index: 2;
  transform: scale(1.05);
  border: 1px solid rgba(255, 255, 255, 1);
  background-color: rgba(255, 255, 255, 0.4);
  transition: .2s;
}

.portraits .active {
  z-index: 3;
  transform: scale(1.15);
  border: 1px solid rgb(255, 198, 57);
  background-color: rgba(240, 100, 20, 1);
  box-shadow: 
    1px 1px 10px rgba(255, 198, 57, 0.5),
    -1px 1px 4px rgb(255, 198, 57, 0.5),
    1px -1px 10px rgb(255, 198, 57, 0.5),
    -1px -1px 4px rgb(255, 198, 57, 0.5);
  transition: .2s;
}

.portraits img,
.abilities img {
  width: 100%;
  height: 100%;
  border-radius: 4px;
  object-fit: contain;
  transition: .2s;
}

.selected-hero {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.selected-hero div {
  width: 45px;
  height: 45px;
  box-sizing: border-box;
  background-color: none;
  border-radius: 4px;
  border: 1px solid rgba(255, 255, 255, 0.2);
  background-color: rgba(0, 0, 0, 0.4);
  backdrop-filter: blur(5px);
  cursor: pointer;
  transition: .2s;
}

button {
  width: max-content;
  padding: 8px 24px 5px 24px;
  box-shadow: 1px 1px 3px rgba(0, 0, 0, .5);
  border-radius: 2px;
  border: none;
  background-color: rgb(240, 107, 38);
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
  background-color: rgb(209, 91, 32);
}
</style>