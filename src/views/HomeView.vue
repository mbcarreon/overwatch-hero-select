<script>
import MainMenuKirikoVideo from '@/assets/videos/MainMenuKiriko.webm';

export default {
  data() {
    return {
      videoSource: MainMenuKirikoVideo
    };
  },
  methods: {
    redirectToHeroSelect() {
      this.$router.push('/heroselect');
    },
    exitGame() {
      // Implement exit game logic, maybe close the app or navigate to an exit page
    },
    goBack() {
      // Navigate back to the home or previous page
      this.$router.go(-1);
    }
  }
}
</script>

<template>
  <div class="homepage">
    <video autoplay loop class="background-video">
      <source :src="videoSource" type="video/webm">
      Your browser does not support the video tag.
    </video>

    <div class="top-left-logo">
      <h1>OVERWATCH 2</h1>
    </div>

    <div class="left-content">
      <h1>Title Here</h1>
      <h2>Subtitle Here</h2>
      <button class="start-button" @click="redirectToHeroSelect">Play/Start</button>
    </div>

    <div class="right-content">
      <div class="hero-preview">
        <!-- Dynamically list heroes here -->
      </div>
      <button class="exit-button" @click="exitGame">Exit Game</button>
      <button class="back-button" @click="goBack">Back to Home</button>
    </div>
  </div>
</template>

<style scoped>
.homepage {
  position: relative;
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 32px;
}

.background-video {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  z-index: -1;
}

.top-left-logo {
  position: absolute;
  top: 50px;
  left: 50px;
  z-index: 10;
  font-family:'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
}

.left-content {
  z-index: 2;
  width: 40%;
}

.right-content {
  z-index: 2;
  width: 40%;
  display: flex;
  flex-direction: column;
  align-items: flex-end;
}

.hero-preview {
  width: 100%;
  height: 300px; /* Adjust based on content */
  margin-bottom: 20px;
  display: flex;
  justify-content: space-around;
  background: rgba(255, 255, 255, 0.1); /* for visibility, remove if unnecessary */
}

.exit-button, .back-button {
  margin-top: 10px;
}

/* Additional styles for buttons, texts, and containers */
</style>
