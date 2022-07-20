<template>
  <section class="container">
    <profile-card @timeframe="timeframeUpdate" />

    <div class="trackers-wrapper" v-if="timeData">
      <div class="trackers" v-for="card in timeData" :key="card.index">

      <tracker-card v-if="timeframe == 'Daily'"
      :title="card.title"
      :hours="card.timeframes.daily.current"
      :previous="card.timeframes.daily.previous"
      :headerImage="card.image"
      :headerColor="card.color" />

      <tracker-card v-if="timeframe == 'Weekly'"
      :title="card.title"
      :hours="card.timeframes.weekly.current"
      :previous="card.timeframes.weekly.previous"
      :headerImage="card.image"
      :headerColor="card.color" />

      <tracker-card v-if="timeframe == 'Monthly'"
      :title="card.title"
      :hours="card.timeframes.monthly.current"
      :previous="card.timeframes.monthly.previous"
      :headerImage="card.image"
      :headerColor="card.color" />

    </div>
    </div>

  </section>
</template>

<script>
import ProfileCard from '~/components/global/ProfileCard.vue'
import TrackerCard from '~/components/global/TrackerCard.vue'
import data from '~/config/data.json'

export default {
  name: 'IndexPage',

  components: { 
    ProfileCard,
    TrackerCard
  },

  data:() => ({
    timeData: data,
    timeframe: 'Daily'
  }),

  methods: {
    timeframeUpdate(payload) {
      this.timeframe = payload
    }
  }
}
</script>

<style lang="scss">
@import '~/assets/_color-palette.scss';

body {
  margin: 0 !important;
  padding: 0 !important;
  box-sizing: border-box !important;
}

.container {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
  height: 110vh;
  width: 100%;
  background-color: colorPaletteSetting(neutral-xtra-dark-blue);

  @media screen and (min-width: 800px ) {
    flex-direction: row;
  }
}

.data {
  color: white;
}


.trackers-wrapper {
display: flex;
flex-direction: column;

  @media screen and (min-width: 1000px ) {
    display: grid;
    grid-template-columns: repeat(3,240px);  /* 3 columns */
    grid-template-rows: repeat(2,240px); /* 3 rows  */
    grid-gap:30px 30px; 
  }
}
</style>
