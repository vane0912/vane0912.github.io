<template>
  <main class="align-homepage">
    <div class="homepage-text">
      <h1 class="h1-blue-styling">Get the latest weather <img class="image-size" alt="cloudy sun" src="@/assets/icons/cloudy.png">results</h1>
      <div class="wrap-BandI">
        <cityInput v-model="city"/>
        <searchButton :to="{name: 'about'}" @searchCountry="weatherResult()" class="adjust-to-input"/>
      </div>
      <div style="display: none;" class="allCities">
        <ul>
          <li v-for="cities in filterCity">{{ cities }}</li>
        </ul>
      </div>
    </div>
    <div class="background-homepage">
      <img class="cards" alt="weather design example" src="@/assets/background-images/weather-cards.svg">
    </div>
  </main>
</template>

<script>
import searchButton from '@/components/button-component.vue';
import cityInput from '@/components/inputCity-component.vue';
export default{
  components: {searchButton, cityInput},
  data(){
    return{
      city: '',
      citiesApi: [],
    }
  },
  computed:{
    filterCity(){
      fetch('https://countriesnow.space/api/v0.1/countries')
      .then(response => response.json())
      .then(data => this.citiesApi = data.data)
      if(this.city.length > 0){
        const toLc = this.citiesApi.map(value => value.country.toLowerCase())
        return toLc.filter(value => value.includes(this.city.toLowerCase()))
      }
    }
  },
  methods:{
    weatherResult(){
      const userCity = this.city;
      this.$route.params.id = userCity;
      this.$router.push({name:'about'})
    },
  }
}
</script>

<style lang="scss">
@use '@/assets/global-mixins.scss';
@import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,200;0,300;0,400;0,500;0,600;0,700;0,800;1,900&display=swap');
body, html, #app, main{
  @include global-mixins.heightAndWidth(100%, 100, #F0F7F4);
  margin: 0;
}
.homepage-text{
  @include global-mixins.heightAndWidth(90vh, 45vw);
  @include global-mixins.positionDisplay(center, column, flex-start)
}
.image-size{
  @include global-mixins.heightAndWidth(80px, 80px)
}
.align-homepage{
  @include global-mixins.positionDisplay(space-evenly, row, center)
}
.background-homepage{
  @include global-mixins.heightAndWidth(80vh, 45vw);
  @include global-mixins.positionDisplay();
  border-radius: 7px;
  animation: moveBackground 30s infinite alternate;
}
.cards{
  @include global-mixins.clamp(29rem, 90%, 80rem, 40rem, 100%, 80rem, transparent,);
}
.adjust-to-input{
  position: relative;
  right: 2%;
}
.wrap-BandI{
  @include global-mixins.heightAndWidth(10%, 100%, transparent);
  @include global-mixins.positionDisplay(flex-start, row, center);
}
.allCities{
  @include global-mixins.heightAndWidth(20vh, 37vw, #23395B);
  @include global-mixins.fontStyling(100, #F0F7F4, 20px);
  border-radius: 5px;
  overflow: scroll;
}
@keyframes moveBackground{
  from{
    @include global-mixins.backgroundimg(url("@/assets/background-images/cloudy-sky.jpg"), 100vw 100%);
    background-position: 0%;
  }
  to{
    @include global-mixins.backgroundimg(url("@/assets/background-images/cloudy-sky.jpg"), 100vw 100%);
    background-position: 100%;
  }
}
@keyframes moveBackgroundmobile{
  from{
    @include global-mixins.backgroundimg(url("@/assets/background-images/cloudy-sky.jpg"), 1000px 100vh);
    background-position: 0%;
  }
  to{
    @include global-mixins.backgroundimg(url("@/assets/background-images/cloudy-sky.jpg"), 1000px 100vh);
    background-position: 100%;
  }
}
@media screen and (max-width: 921px) {
    .align-homepage{
      @include global-mixins.heightAndWidth(100%, 100%);
      animation: moveBackgroundmobile 30s infinite alternate;
    }
    .cards, .background-homepage{
      display: none;
    }
    .homepage-text{
      @include global-mixins.heightAndWidth(80%, 80%);
      @include global-mixins.positionDisplay(center, column, center);
      padding: 5%;
      border-radius: 17px;
    }
    .h1-blue-styling{
      @include global-mixins.fontStyling(800, #23395B, 55px);
      text-align: center;
      margin: 10% 0%;
    }
    .image-size{
      position: absolute;
      top: 10%;
      left: 45%;
    }
    .wrap-BandI{
      @include global-mixins.positionDisplay(space-between, column, center);
      @include global-mixins.heightAndWidth(20%, 100%, transparent);
    }
    .adjust-to-input{
      margin: 10px;
      border: none;
      filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
    }
}
@media screen and (max-width: 500px){
  .image-size{
      left: 40%;
  }
}
</style>