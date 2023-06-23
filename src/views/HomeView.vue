<template>
  <main class="align-homepage">
    <div class="align-elements">
      <div class="homepage-text">
        <div class="image-h1-mobile">
          <img class="image-size" alt="cloudy sun" src="@/assets/icons/cloudy.png">
          <h1 class="h1-blue-styling">Get the latest weather results</h1>
        </div>
        <h1 class="h1-blue-styling image-h1-desktop">Get the latest weather <img class="image-size" alt="cloudy sun" src="@/assets/icons/cloudy.png">results</h1>
        <cityInput 
        />
      </div>
      <div class="background-homepage">
        <img class="cards" alt="weather design example" src="@/assets/background-images/weather-cards.svg">
      </div>
    </div>
  </main>
</template>

<script>
import cityInput from '@/components/inputCity-component.vue';
export default{
  components: {cityInput},
  data(){
    return{
      inputValue: "",
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
.align-elements{
  @include global-mixins.minMax(100%, 1900px, 100%, 1000px, transparent);
  @include global-mixins.positionDisplay(space-evenly, row, center);
}
.homepage-text{
  @include global-mixins.heightAndWidth(100%, 45%);
  @include global-mixins.positionDisplay(center, column, center)
}
.image-size{
  @include global-mixins.heightAndWidth(80px, 80px)
}
.align-homepage{
  @include global-mixins.positionDisplay(space-evenly, row, center);
}
.background-homepage{
  @include global-mixins.heightAndWidth(80%, 43%);
  @include global-mixins.positionDisplay();
  border-radius: 7px;
  animation: moveBackground 30s infinite alternate;
}
.cards{
  @include global-mixins.minMax(90%, 80rem, 100%, 80rem, transparent,);
}
.adjust-to-input{
  position: relative;
  right: 2%;
}
.wrap-BandI{
  @include global-mixins.heightAndWidth(50%, 100%, transparent);
  @include global-mixins.positionDisplay(flex-start, row, center);
}
.image-h1-mobile{
  display: none
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
    @include global-mixins.backgroundimg(url("@/assets/background-images/cloudy-sky.jpg"), 1000px 100%);
    background-position: 0%;
  }
  to{
    @include global-mixins.backgroundimg(url("@/assets/background-images/cloudy-sky.jpg"), 1000px 100%);
    background-position: 100%;
  }
}
@media screen and (max-width: 1023px) {
  .image-h1-mobile{
    display: block;
    @include global-mixins.positionDisplay(center, column, center);
  }
  .align-homepage{
    @include global-mixins.heightAndWidth(100%, 100%);
    animation: moveBackgroundmobile 30s infinite alternate;
  }
  .cards, .background-homepage, .image-h1-desktop{
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
</style>