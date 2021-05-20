<template>
  <div>
    <div :class="['details', show ? 'details-slide' : '']">
      <div class="details-header">
        <div>{{ serie.title }}</div>
        <svg
          @click="close"
          t="1621207740203"
          class="close-icon"
          viewBox="0 0 1025 1024"
          version="1.1"
          xmlns="http://www.w3.org/2000/svg"
          p-id="1482"
          width="64"
          height="64"
        >
          <path
            d="M513.344 0a512 512 0 1 0 0 1024 512 512 0 0 0 0-1024z m226.048 674.624l-54.528 56.896-171.52-164.928-171.392 164.928-54.592-56.896L456.576 512 287.36 349.312l54.592-56.768 171.392 164.8 171.52-164.8 54.528 56.768L570.176 512l169.216 162.624z"
            fill="#e6e6e6"
            p-id="1483"
          ></path>
        </svg>
      </div>
      <div class="details-box">
        <Player
          :pause="pause"
          :episode="serie.episodes ? serie.episodes[currentEpisode] : {}"
          @restorePauseStatus="restorePauseStatus"
        />
        <div
          v-if="serie.episodes && serie.episodes.length"
          class="episode-list"
        >
          <div class="episode">选集</div>
          <div class="selector">
            <div class="selector-box">
              <div
                v-for="(episode, index) in serie.episodes"
                :key="index"
                :class="[
                  'selector-child',
                  currentEpisode === index ? 'selected-child' : ''
                ]"
                @click="selectEpisode(index)"
              >
                {{ index + 1 }}
              </div>
            </div>
          </div>
          <div class="episode-title">
            {{
              serie.episodes[currentEpisode].title
                ? serie.episodes[currentEpisode].title
                : ''
            }}
          </div>
          <div class="episode-desc">
            {{
              serie.episodes[currentEpisode].desc
                ? serie.episodes[currentEpisode].desc
                : ''
            }}
          </div>
        </div>
      </div>
    </div>
    <div :class="['mask', show ? 'mask-fade' : '']" @click="close"></div>
  </div>
</template>

<script>
import Player from './Player';
export default {
  name: 'Details',
  components: {
    Player
  },
  props: {
    show: Boolean,
    serie: Object
  },
  watch: {
    serie(newVal) {
      if (newVal !== undefined) {
        this.currentEpisode = 0;
      }
    }
  },
  data() {
    return {
      pause: false,
      currentEpisode: 0
    };
  },
  methods: {
    close() {
      this.pause = true;
      this.$emit('closeDetails');
    },
    restorePauseStatus() {
      this.pause = false;
    },
    selectEpisode(index) {
      this.currentEpisode = index;
    }
  }
};
</script>

<style scoped>
.details {
  width: 100%;
  z-index: 1000;
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #040b13;
  will-change: transform;
  transition: transform ease 0.3s;
  transform: translate3d(0, 100%, 0);
  padding-bottom: constant(safe-area-inset-bottom);
  padding-bottom: env(safe-area-inset-bottom);
  border-radius: 16px 16px 0 0;
  color: #e6e6e6;
}

.details-slide {
  transform: translate3d(0, 0, 0);
}

.details-header {
  display: flex;
  justify-content: space-between;
  font-size: 1rem;
  line-height: 1.2rem;
  font-weight: bold;
  padding: 0.8rem 1rem;
  align-items: center;
  height: 1.2rem;
}

.mask {
  display: none;
  touch-action: none;
  width: 100%;
  height: 100%;
  background-color: rgba(35, 35, 35, 0.5);
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: 998;
  will-change: animation;
  transition: animation;
  animation: fadeIn ease 0.3s forwards;
}

.mask-fade {
  display: block;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.close-icon {
  width: 1.2rem;
  height: 1.2rem;
}

.details-box {
  max-height: 85vh;
  overflow-y: scroll;
}

.episode-list {
  padding: 1rem;
}

.episode-list > .episode {
  font-size: 1rem;
  font-weight: bold;
}

.episode-list > .selector {
  width: calc(100% - 2rem);
  overflow: scroll;
  padding: 1rem;
  margin-top: 0.8rem;
  background-color: #1d232b;
  border-radius: 1.5rem;
  display: flex;
}

.details-box::-webkit-scrollbar,
.selector::-webkit-scrollbar {
  display: none;
}

.selector-box {
  width: auto;
  display: flex;
  align-items: center;
}

.selector-child {
  width: 3rem;
  height: 3rem;
  background-color: #81d8d0;
  border-radius: 1.2rem;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-shrink: 0;
  font-size: 1.2rem;
  font-weight: bold;
  margin-right: 1rem;
}

.selector > .selector-child:last-child {
  margin-right: 0;
}

.selected-child {
  background-color: #6495ed;
}

.episode-title {
  font-size: 1rem;
  margin-top: 1.2rem;
}

.episode-desc {
  font-size: .9rem;
  margin: 0.8rem 0;
  line-height: 1.2;
}
</style>
