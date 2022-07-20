<template>
  <section class="tracker-card">
    <div class="tracker-card-upper" :class="`tracker-card-upper-${headerColor}`">
      <img :src="headerImage" alt="">
    </div>
    <div class="tracker-card-lower">
      <div class="tracker-card-lower__upper">
        <p class="tracker-card-lower__upper-title">{{title}}</p>
        <img class="icon" src="/images/icon-ellipsis.svg" alt="">
      </div>
      <div class="tracker-card-lower__lower">
        <p class="tracker-card-lower__lower-hour">{{hours}}hrs</p>
        <p class="tracker-card-lower__lower-previous">Last Week - {{previous}}hrs</p>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'tracker-card',

  props: {
    title: {
      type: String,
      required: true
    },
    hours: {
      type: String,
      required: true
    },
    previous: {
      type: String,
      required: true
    },
    headerImage: {
      type: String,
      required: true
    },
    headerColor: {
      type: String,
      required: true
    }
  }
}
</script>

<style lang="scss">
@import '~/assets/_color-palette.scss';
@import '~/assets/abstract.scss';

.tracker-card {

  &-upper {
    position: relative;
    top: 20px;
    height: 60px;
    width: 327px;
    background-color: green;
    border-top-left-radius: 15px;
    border-top-right-radius: 15px;
    display: flex;
    justify-content: flex-end;

    @media screen and (min-width: 400px ) {
      width: 255px;
      height: 65px;
    }
  }

  &-lower {
    position: relative;
    z-index: 1;
    background-color: colorPaletteSetting(neutral-dark-blue);
    height: 125px;
    width: 327px;
    border-radius: 15px;

    @media screen and (min-width: 400px ) {
      height: 200px;
      width: 255px;
    }

    &__upper {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 0 20px;
      height: 50px;
      // background-color: blue;

      &-title {
        font-family: abstractSetting(primary_font);
        color: white;
      }
    }

    &__lower{
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 0 20px;

      @media screen and (min-width: 400px ) {
        flex-direction: column;
        align-items: flex-start;
      }

      &-hour {
        font-size: 40px;
        font-family: abstractSetting(primary_font);
        color: white;
        margin: 20px 0;
      }

      &-previous {
        font-size: 12px;
        font-family: abstractSetting(primary_font);
        color: white;
        margin: 0;
      }
    }
  }
}
.icon {
  height: 4px;
}

.tracker-card-upper {

  &-orange {
    background-color: colorPaletteSetting(primary-light-red-work)
  }

  &-blue {
    background-color: colorPaletteSetting(primary-light-blue);
  }

  &-pink {
    background-color: colorPaletteSetting(primary-light-red-study);
  }

  &-green {
    background-color: colorPaletteSetting(primary-lime-green);
  }

  &-purple {
    background-color: colorPaletteSetting(primary-violet);
  }

  &-yellow {
    background-color: colorPaletteSetting(primary-orange);
  }
}
</style>