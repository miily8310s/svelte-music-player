<script lang="ts">
let audio: HTMLAudioElement;
let progress: HTMLElement;
let title: string;
let paused = true;
let duration: number;
let currentTime: number;
let width: number;

title = "ukulele";

const playSong = () => {
  audio.play();
};

const pauseSong = () => {
  audio.pause();
};

const onClickPlayButton = () => {
  if (!paused) {
    pauseSong();
  } else {
    playSong();
  }
  paused = !paused;
};

const updateProgress = () => {
  const progressPercent = (currentTime / duration) * 100;
  progress.style.width = `${progressPercent}%`;
};

const onClickSetProgress = (e: MouseEvent) => {
  const clickX = e.offsetX;
  audio.currentTime = (clickX / width) * duration;
};
</script>

<h1>Music Player</h1>
<div class="music-container">
  <div class="music-info">
    <h4 contenteditable="true" bind:textContent="{title}"></h4>
    <div
      class="progress-container"
      bind:clientWidth="{width}"
      on:click="{onClickSetProgress}"
    >
      <div class="progress" bind:this="{progress}"></div>
    </div>
  </div>
  <audio
    src="/music/ukulele.mp3"
    bind:this="{audio}"
    on:timeupdate="{updateProgress}"
    bind:duration
    bind:currentTime></audio>
  <div class="img-container">
    <img
      src="/images/ukulele.jpg"
      alt="music-cover"
      id="cover"
      style="animation-play-state: {paused ? 'paused' : 'running'}"
    />
  </div>
  <div class="navigation">
    <button id="prev" class="action-btn">
      <i class="fas fa-backward"></i>
    </button>
    <button class="action-btn action-btn-big" on:click="{onClickPlayButton}">
      <i class="{!paused ? 'fas fa-pause' : 'fas fa-play'}"></i>
    </button>
    <button id="next" class="action-btn">
      <i class="fas fa-forward"></i>
    </button>
  </div>
</div>

<style type="text/scss">
@import "./Player.scss";
</style>
