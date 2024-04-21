<template>
  <div class="main-container">
    <video autoplay muted loop id="background-video">
      <source src="./assets/videos/Kiriko.mp4" type="video/mp4">
    </video>
    <div class="hero-details-container">
      <h2>Support</h2>
      <h1>Kiriko</h1>
      <div class="abilities-container">
        <div class="abilities-sub-container"></div>
        <div class="abilities-sub-container"></div>
        <div class="abilities-sub-container"></div>
        <div class="abilities-sub-container"></div>
        <div class="abilities-sub-container"></div>
        <div class="abilities-sub-container"></div>
      </div>
      <h3>Healing Ofuda</h3>
      <h4>Channel a burst of healing talismans that can seek targeted allies.</h4>
    </div>
    <div class="heroes-container">
      <div class="heroes-sub-container" v-for="hero in heroes" :key="hero.id" @click="changeBackground()">
        <img :src="hero.profile">
      </div>
    </div>
    <div class="button-container">
      <button>Select</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const heroes = ref([
  { id: 1, name: 'Ana', profile: '/src/assets/images/Ana.png', background: '/src/videos/images/Ana.mp4' },
  { id: 2, name: 'Ashe', profile: '/src/assets/images/Ashe.png', background: '/src/videos/images/Ashe.mp4' },
  { id: 3, name: 'Baptiste', profile: '/src/assets/images/Baptiste.png', background: '/src/videos/images/Baptiste.mp4' },
  { id: 4, name: 'Bastion', profile: '/src/assets/images/Bastion.png', background: '/src/videos/images/Bastion.mp4' },
  { id: 5, name: 'Brigitte', profile: '/src/assets/images/Brigitte.png', background: '/src/videos/images/Brigitte.mp4' },
  { id: 6, name: 'Cassidy', profile: '/src/assets/images/Cassidy.png', background: '/src/videos/images/Cassidy.mp4' },
  { id: 7, name: 'D.Va', profile: '/src/assets/images/Dva.png', background: '/src/videos/images/Dva.mp4' },
  { id: 8, name: 'Doomfist', profile: '/src/assets/images/Doomfist.png', background: '/src/videos/images/Doomfist.mp4' },
  { id: 9, name: 'Echo', profile: '/src/assets/images/Echo.png', background: '/src/videos/images/Echo.mp4' },
  { id: 10, name: 'Genji', profile: '/src/assets/images/Genji.png', background: '/src/videos/images/Genji.mp4' },
  { id: 11, name: 'Hanzo', profile: '/src/assets/images/Hanzo.png', background: '/src/videos/images/Hanzo.mp4' },
  { id: 12, name: 'Illari', profile: '/src/assets/images/Illari.png', background: '/src/videos/images/Illari.mp4' },
  { id: 13, name: 'Junker Queen', profile: '/src/assets/images/JunkerQueen.png', background: '/src/videos/images/JunkerQueen.mp4' },
  { id: 14, name: 'Junkrat', profile: '/src/assets/images/Junkrat.png', background: '/src/videos/images/Junkrat.mp4' },
  { id: 15, name: 'Kiriko', profile: '/src/assets/images/Kiriko.png', background: '/src/videos/images/Kiriko.mp4' },
  { id: 16, name: 'Lifeweaver', profile: '/src/assets/images/Lifeweaver.png', background: '/src/videos/images/Lifeweaver.mp4' },
  { id: 17, name: 'Lúcio', profile: '/src/assets/images/Lucio.png', background: '/src/videos/images/Lucio.mp4' },
  { id: 18, name: 'Mauga', profile: '/src/assets/images/Mauga.png', background: '/src/videos/images/Mauga.mp4' },
  { id: 19, name: 'Mei', profile: '/src/assets/images/Mei.png', background: '/src/videos/images/Mei.mp4' },
  { id: 20, name: 'Mercy', profile: '/src/assets/images/Mercy.png', background: '/src/videos/images/Mercy.mp4' },
  { id: 21, name: 'Moira', profile: '/src/assets/images/Moira.png', background: '/src/videos/images/Moira.mp4' },
  { id: 22, name: 'Orisa', profile: '/src/assets/images/Orisa.png', background: '/src/videos/images/Orisa.mp4' },
  { id: 23, name: 'Pharah', profile: '/src/assets/images/Pharah.png', background: '/src/videos/images/Pharah.mp4' },
  { id: 24, name: 'Ramattra', profile: '/src/assets/images/Ramattra.png', background: '/src/videos/images/Ramattra.mp4' },
  { id: 25, name: 'Reaper', profile: '/src/assets/images/Reaper.png', background: '/src/videos/images/Reaper.mp4' },
  { id: 26, name: 'Reinhardt', profile: '/src/assets/images/Reinhardt.png', background: '/src/videos/images/Reinhardt.mp4' },
  { id: 27, name: 'Roadhog', profile: '/src/assets/images/Roadhog.png', background: '/src/videos/images/Roadhog.mp4' },
  { id: 28, name: 'Sigma', profile: '/src/assets/images/Sigma.png', background: '/src/videos/images/Sigma.mp4' },
  { id: 29, name: 'Sojourn', profile: '/src/assets/images/Sojourn.png', background: '/src/videos/images/Sojourn.mp4' },
  { id: 30, name: 'Soldier: 76', profile: '/src/assets/images/Soldier76.png', background: '/src/videos/images/Soldier76.mp4' },
  { id: 31, name: 'Sombra', profile: '/src/assets/images/Sombra.png', background: '/src/videos/images/Sombra.mp4' },
  { id: 32, name: 'Symmetra', profile: '/src/assets/images/Symmetra.png', background: '/src/videos/images/Symmetra.mp4' },
  { id: 33, name: 'Torbjörn', profile: '/src/assets/images/Torbjorn.png', background: '/src/videos/images/Torbjorn.mp4' },
  { id: 34, name: 'Tracer', profile: '/src/assets/images/Tracer.png', background: '/src/videos/images/Tracer.mp4' },
  { id: 35, name: 'Widowmaker', profile: '/src/assets/images/Widowmaker.png', background: '/src/videos/images/Widowmaker.mp4' },
  { id: 36, name: 'Winston', profile: '/src/assets/images/Winston.png', background: '/src/videos/images/Winston.mp4' },
  { id: 37, name: 'Wrecking Ball', profile: '/src/assets/images/WreckingBall.png', background: '/src/videos/images/WreckingBall.mp4' },
  { id: 38, name: 'Zarya', profile: '/src/assets/images/Zarya.png', background: '/src/videos/images/Zarya.mp4' },
  { id: 39, name: 'Zenyatta', profile: '/src/assets/images/Zenyatta.png', background: '/src/videos/images/Zenyatta.mp4' }
]);
</script>

<style scoped>
* {
  color: white;
  font-family: "Bebas";
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
}

.hero-details-container {
  width: 30%;
  display: flex;
  flex-direction: column;
}

h1, h2, h3 {
  margin: 0;
  padding: 0;
  line-height: 0.8;
}

h1 {
  font-size: 5.8rem;
  margin-top: 8px;
  margin-bottom: 32px;
}

h2 {
  font-size: 2.8rem;
}

h3 {
  font-size: 1.8rem;
  margin-top: 24px;
  margin-bottom: 16px;
}

h4 {
  font-family: "Roboto";
  font-size: 1rem;
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
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  margin: auto;
  margin-top: 220px;
}

.heroes-sub-container {
  width: 55px;
  height: 55px;
  background-color: rgba(1, 1, 1, .70);
  border: 2px solid rgb(190, 190, 190);
  border-radius: 4px;
  transition: 0.3s;
  cursor: pointer;
}

.heroes-sub-container:hover {
  transition: 0.3s;
  transform: scale(1.1);
}

.heroes-sub-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 4px;
}

.button-container {
  margin: auto;
  margin-top: 32px;
}

button {
  width: max-content;
  padding: 12px 16px 8px 16px;
  background-color: rgb(50, 255, 253);
  color: 2px solid rgb(190, 190, 190);
  font-family: "Bebas Neue";
  text-transform: uppercase;
  font-size: 1.5rem;
  letter-spacing: 2px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
</style>
