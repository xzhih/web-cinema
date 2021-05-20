<template>
  <div class="hello">
    <video id="player" playsinline controls>
      <source src="" type="video/mp4" />
    </video>
  </div>
</template>

<script>
import Plyr from 'plyr';

export default {
  name: 'Player',
  props: {
    pause: {
      type: Boolean,
      default() {
        return false;
      }
    },
    episode: Object
  },
  watch: {
    pause(newVal) {
      if (newVal !== undefined) {
        if (newVal) {
          this.player.pause();
          this.restorePauseStatus();
        }
      }
    },
    episode(newVal) {
      if (newVal !== undefined) {
        if (newVal.src) {
          this.player.source = {
            type: 'video',
            sources: [
              {
                title: newVal.title || '',
                src: newVal.src,
                type: 'video/mp4',
                size: 1080
              }
            ],
            poster: newVal.poster || ''
          };
        }
      }
    }
  },
  mounted() {
    this.player = new Plyr('#player', {
      controls: [
        'play-large', // The large play button in the center
        'rewind', // Rewind by the seek time (default 10 seconds)
        'play', // Play/pause playback
        'fast-forward', // Fast forward by the seek time (default 10 seconds)
        'progress', // The progress bar and scrubber for playback and buffering
        'current-time', // The current time of playback
        'duration', // The full duration of the media
        'settings', // Settings menu
        'pip', // Picture-in-picture (currently Safari only)
        'fullscreen' // Toggle fullscreen
      ],
      fullscreen: {
        enabled: true,
        fallback: true,
        iosNative: true,
        container: null
      },
      speed: { selected: 1, options: [0.5, 0.75, 1, 1.25, 1.5, 1.75, 2] },
      i18n: {
        settings: '设置',
        speed: '速度',
        normal: '1x'
      }
    });
  },
  methods: {
    restorePauseStatus() {
      this.$emit('restorePauseStatus');
    }
  }
};
</script>

<style scoped></style>
