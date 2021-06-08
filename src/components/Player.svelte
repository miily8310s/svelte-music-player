<script lang="ts">
let audio: HTMLAudioElement;
let paused = false;

const playSong = () => {
  audio.play();
};

// Pause song
const pauseSong = () => {
  audio.pause();
};

const onClickPlayButton = () => {
  if (!paused) {
    playSong();
  } else {
    pauseSong();
  }
  paused = !paused;
};
</script>

<h1>Music Player</h1>
<div class="music-container">
  <div class="music-info">
    <h4 id="title"></h4>
    <div class="progress-container" id="progress-container">
      <div class="progress" id="progress"></div>
    </div>
  </div>
  <audio src="/music/ukulele.mp3" id="audio" bind:this="{audio}"></audio>
  <div class="img-container">
    <img src="/images/ukulele.jpg" alt="music-cover" id="cover" />
  </div>
  <div class="navigation">
    <button id="prev" class="action-btn">
      <i class="fas fa-backward"></i>
    </button>
    <button
      id="play"
      class="action-btn action-btn-big"
      on:click="{onClickPlayButton}"
    >
      <i class="{paused ? 'fas fa-pause' : 'fas fa-play'}"></i>
    </button>
    <button id="next" class="action-btn">
      <i class="fas fa-forward"></i>
    </button>
  </div>
</div>

<style type="text/scss">
@import "./Player.scss";
</style>
