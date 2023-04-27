<template>
    <main class="align-homepage">
        <div class="homepage-text">
            <h1 class="h1-styling">Get the latest weather <img class="image-size" alt="cloudy sun" src="@/assets/icons/cloudy.png"> results</h1>
            <div class="wrap-BandI">
              <cityInput/>
              <searchButton class="adjust-to-input"/>
            </div>
        </div>
        <div class="background-homepage">
          <img class="cards" alt="weather design example" src="@/assets/background-images/weather-cards.svg">
        </div>
    </main>
</template>

<script>
import searchButton from '@/components/button-component.vue';
import cityInput from '@/components/input-component.vue';
  export default{
    components: {searchButton, cityInput},
    data(){
      return{
        city: ''
      }
    },  
    methods:{
      showAnimation(){
        const userCity = this.city
        fetch(`https://goweather.herokuapp.com/weather/${userCity}`)
        .then(res => res.json())
        .then(data => console.log(data.temperature))
      }
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
  .h1-styling{
    @include global-mixins.fontStyling(800, #23395B, 80px);
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
    @include global-mixins.heightAndWidth(80%, 70%, transparent);
  }
  .adjust-to-input{
    position: relative;
    right: 2%;
  }
  .wrap-BandI{
    @include global-mixins.heightAndWidth(10vh, 40vw);
    @include global-mixins.positionDisplay(flex-start, row, center);
  }
  @keyframes moveBackground{
    from{
      background-image: url("@/assets/background-images/cloudy-sky.jpg");
      background-position: 0% 100%;
      background-size: 100vw 100%;
    }
    to{
      background-image: url("@/assets/background-images/cloudy-sky.jpg");
      position: relative;
      background-position: 100% 100%;
      background-size: 100vw 100%;
    }
  }
  @keyframes moveBackgroundmobile{
    from{
      background-image: url("@/assets/background-images/cloudy-sky.jpg");
      background-position: 0% 100%;
      background-size: 1000px 100vh;
    }
    to{
      background-image: url("@/assets/background-images/cloudy-sky.jpg");
      position: relative;
      background-position: 100% 100%;
      background-size: 1000px 100vh;
    }
  }
  @media screen and (min-width: 2560px){
    .wrap-BandI{
        @include global-mixins.heightAndWidth(8%, 100%, transparent);
    }
  }
  @media screen and (max-width: 900px) {
      main{
        @include global-mixins.heightAndWidth(100vh, 100vw);
        animation: moveBackgroundmobile 30s infinite alternate;
      }
      .cards, .background-homepage{
        display: none;
      }
      .homepage-text{
        @include global-mixins.heightAndWidth(80vh, 80vw);
        @include global-mixins.positionDisplay(center, column, center);
        padding: 5%;
        border-radius: 17px;
      }
      .h1-styling{
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
