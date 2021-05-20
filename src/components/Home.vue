<template>
  <div>
    <div class="home-wrap">
      <div
        v-for="(series, index) in seriesList"
        :key="index"
        class="movies-card"
        @click="showDtails(index)"
      >
        <img class="season-cover" mode="aspectFill" :src="series.poster" />
        <div class="season-title">{{ series.title }}</div>
      </div>
    </div>
    <Details
      :show="detailsStatus"
      :serie="seletedSerie"
      @closeDetails="closeDetails"
    />
  </div>
</template>

<script>
import Details from './Details';
import seriesList from '../seriesList';
export default {
  name: 'Home',
  components: {
    Details
  },
  data() {
    return {
      detailsStatus: false,
      seletedSerie: {},
      seriesList: seriesList
    };
  },
  methods: {
    showDtails(index) {
      this.seletedSerie = this.seriesList[index];
      this.detailsStatus = true;
    },
    closeDetails() {
      this.detailsStatus = false;
    }
  }
};
</script>

<style scoped>
* {
  user-select: none;
}

.movies-card {
  width: calc(100% - 2rem);
  margin: 1rem 1rem 0 1rem;
  border: 1px solid rgba(227, 227, 227, 0.3);
  border-radius: 8px;
  background-color: #040b13;
  box-sizing: border-box;
}

.season-cover {
  width: 100%;
  border-radius: 8px 8px 0 0;
  display: flex;
}

.season-title {
  font-size: 1.1rem;
  font-weight: bold;
  padding: 0.75rem 1rem;
}

@media screen and (min-width: 540px) {
  .home-wrap {
    display: flex;
    flex-flow: row wrap;
    align-content: flex-start;
  }
  .movies-card {
    flex: 0 0 calc(50% - 1.5rem);
    margin: 1rem 0.5rem 0 1rem;
  }

  .movies-card:nth-child(even) {
    margin-left: 0.5rem;
  }
}
</style>
