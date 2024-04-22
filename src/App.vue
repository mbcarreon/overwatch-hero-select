<script setup>
import { ref } from 'vue';
import heroesData from './heroes.json';

const heroes = ref(heroesData);

const videoRef = ref(null);

const currentHero = ref(0);

const changeHero = (id) => {
  currentHero.value = id - 1;
  const video = videoRef.value;
  video.load();
};
</script>

<template>
  <div class="main-container">
    <video autoplay muted loop id="background-video" ref="videoRef">
      <source :src="heroes[currentHero].background" type="video/mp4">
    </video>
    <div class="hero-details-container">
      <h2>{{ heroes[currentHero].role }}</h2>
      <h1>{{ heroes[currentHero].name }}</h1>
      <div class="abilities-container">
        <div class="abilities-sub-container"></div>
        <div class="abilities-sub-container"></div>
        <div class="abilities-sub-container"></div>
        <div class="abilities-sub-container"></div>
        <div class="abilities-sub-container"></div>
      </div>
      <h3>Ability</h3>
      <h4>Lorem ipsum</h4>
    </div>
    <div class="heroes-container">
      <div class="heroes-sub-container" v-for="hero in heroes" :key="hero.id" @click="changeHero(hero.id)">
        <img :src="hero.portrait">
      </div>
    </div>
    <div class="button-container">
      <button>Select</button>
    </div>
  </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Figtree:wght@300&family=Instrument+Serif:ital@0;1&display=swap');

* {
  color: white;
  font-family: "Bebas Neue";
}

.main-container {
  width: 100%;
  padding: 48px;
  display: flex;
  flex-direction: column;
}

#background-video {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  z-index: -1;
  transition: .5s;
}

.hero-details-container {
  width: 40%;
  display: flex;
  flex-direction: column;
}

h1, h2, h3 {
  margin: 0;
  padding: 0;
  line-height: 0.8;
  text-transform: uppercase;
  letter-spacing: 2px;
}

h1 {
  font-size: 6rem;
  margin-top: 16px;
  margin-bottom: 32px;
}

h2 {
  font-size: 3.5rem;
}

h3 {
  font-size: 2rem;
  margin-top: 24px;
  margin-bottom: 8px;
}

h4 {
  font-family: "Roboto";
  font-size: 1rem;
  letter-spacing: .8px;
}

.abilities-container {
  display: flex;
  flex-direction: row;
  gap: 12px;
}

.abilities-sub-container {
  width: 55px;
  height: 55px;
  background-color: rgb(190, 190, 190, .70);
  border: 2px solid rgb(190, 190, 190);
  border-radius: 100%;
  transition: 0.3s;
  cursor: pointer;
}

.heroes-container {
  width: 90%;
  height: max-content;
  display: flex;
  flex-wrap: wrap;
  gap: 14px;
  margin: auto;
  margin-top: 220px;
}

.heroes-sub-container {
  width: 55px;
  height: 55px;
  background-color: rgba(1, 1, 1, .50);
  border: 2px solid rgb(190, 190, 190);
  border-radius: 6px;
  transition: 0.3s;
  cursor: pointer;
}

.heroes-sub-container:hover {
  transition: 0.3s;
  transform: scale(1.15);
}

.heroes-sub-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 6px;
}

.button-container {
  margin: auto;
  margin-top: 32px;
}

button {
  width: max-content;
  padding: 12px 24px 8px 24px;
  background-color: rgb(0, 220, 217);
  color: 2px solid rgb(255, 255, 255);
  font-size: 1.5rem;
  letter-spacing: 2px;
  text-align: center;
  border: none;
  border-radius: 8px;
  cursor: pointer;
}
</style>