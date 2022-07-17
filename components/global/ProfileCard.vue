<template>
  <section v-if="userImage && profileData" class="profile-card">
    <div class="profile-card-upper">
      <div class="profile-card-upper__info">
        <img v-if="userImage" class="profile-card-upper__image" :src="userImage" alt="">

        <div class="profile-card-upper__text">
          <p class="profile-card-upper__label">Report for</p>

          <div v-if="firstName && lastName" class="profile-card-upper__name">
            <p class="profile-card-upper__firstName">{{firstName}}</p>
            <p class="profile-card-upper__lastName">{{lastName}}</p>
          </div>
        </div>
      </div>
    </div>

    <div class="profile-card-lower">
      <div class="profile-card-lower__info" v-for="(button, index) in activeButton" :key="button.value">
        <a class="profile-card-lower__button" :class="{'button--active': activeState == index}" @click="showActiveState(index, button.label)">{{button.label}}</a>
      </div>
    </div>
  </section>
</template>

<script>
import axios from 'axios'
import data from '~/config/data.json'

export default {
  name: 'profile-card',

  data:() => ({
    profileData: data,
    userImage: null,
    firstname: null,
    lastName: null,
    activeState: null,
    activeButton: [
      {
        label: 'Daily',
        active: false,
        value: 1
      },
      {
        label: 'Weekly',
        active: false,
        value: 2
      },
      {
        label: 'Monthly',
        active: false,
        value: 3
      }
    ]
  }),

  created() {
    this.getRandomUser()
  },

  methods: {
    getRandomUser() {
      axios.get('https://randomuser.me/api/')
        .then((res) => {
          console.log('User Found', res)
          this.userImage = res.data.results[0].picture.medium
          this.firstName = res.data.results[0].name.first
          this.lastName = res.data.results[0].name.last
        })
        .catch(console.log('No User Found'))

    },

    showActiveState(index, label) {
      this.activeState = index
      this.$emit('timeframe', label)
    }
  }
}
</script>

<style lang="scss">
@import '~/assets/_color-palette.scss';
@import '~/assets/abstract.scss';

.profile-card {
font-family: abstractSetting(primary_font);

  @media screen and (min-width: 800px ) {
    margin-right: 20px;
    margin-top: 70px;
  }

  &-upper {
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    height: 132px;
    width: 327px;
    background-color: colorPaletteSetting(primary-blue);
    border-radius: 15px;
    z-index: 1;

    @media screen and (min-width: 400px ) {
      height: 355px;
      width: 255px;
    }

    &__info {
      display: flex;
      justify-content: space-between;
      align-items: center;
      width: 250px;

      @media screen and (min-width: 400px ) {
        display: block;
        width: 170px;
        margin-bottom: 50px;
      }
    }

    &__label {
      font-size: 12px;
      font-weight: 200;
      color: colorPaletteSetting(neutral-pale-blue);
    }

    &__name {
      display: flex;

      @media screen and (min-width: 400px ) {
        display: block;
      }
    }

    &__firstName {
      font-size: 18px;
      color: white;
      margin: 0;

      @media screen and (min-width: 400px ) {
        font-size: 30px;
      }
    }

    &__lastName {
      font-size: 18px;
      color: white;
      margin: 0;
      padding-left: 10px;

      @media screen and (min-width: 400px ) {
        font-size: 30px;
        padding: 0;
      }
    }

    &__image {
      border-radius: 50%;
      border: solid white 3px;

      @media screen and (min-width: 400px ) {
        margin-bottom: 30px;
      }
    }
  }

  &-lower {
    position: relative;
    display: flex;
    justify-content: center;
    flex-direction: row;
    align-items: center;
    text-align: center;
    top: -20px;
    width: 327px;
    height: 70px;
    background-color: colorPaletteSetting(neutral-dark-blue);
    border-bottom-right-radius: 15px;
    border-bottom-left-radius: 15px;

    @media screen and (min-width: 400px ) {
      height: 185px;
      width: 255px;
      flex-direction: column;
      text-align: left;
    }

    &__info {
      display: flex;
      flex-direction: column;
      justify-content: space-evenly;
      height: 40px;
      font-weight: 200;
      position: relative;
      width: 170px;
      color: colorPaletteSetting(neutral-pale-blue);
      font-size: 15px;
    }

    &__button {
      cursor: pointer;
      margin-top: 15px;

      @media screen and (min-width: 400px ) {
        margin-top: 0;
      }
    }
  }
}

.button--active {
  color: white;
}
</style>