<template>
  <main>
    <div class="align-column">
      <div class="temp-input">
        <cityInput/>
        <searchButton class="adjust-button"/>
      </div>
      <div class="weather-card">
        <div class="icon-description">
          <div class="sunny-icon"></div>
          <h3 class="h3-white-styling">{{ $route.params.id }}</h3>
        </div>
        <div class="temp-and-wind">
          <h2 class="h2-white-styling"> {{ description }} {{ temperature }}</h2>
          <h4 class="h4-white-styling">{{ day }}</h4>
        </div>
      </div>
      <div class="forecasts">
        <div class="grid-childs child1">
          <div class="sunny-icon"></div>
          <div class="mobile-forecast">
            <h3 class="h3-white-styling">{{ day }}</h3>
            <h4 class="h4-white-styling"> {{ forecast1 }}</h4>
          </div>
        </div>
        <div class="grid-childs child2">
          <div class="sunny-icon"></div>
          <div class="mobile-forecast">
            <h3 class="h3-white-styling">{{ day }}</h3>
            <h2 class="h4-white-styling"> {{ forecast2 }}</h2>
          </div>
        </div>
        <div class="grid-childs child3">
          <div class="sunny-icon"></div>
          <div class="mobile-forecast">
            <h3 class="h3-white-styling">{{ day }}</h3>
            <h2 class="h4-white-styling"> {{ forecast3 }}</h2>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>
<script >
import searchButton from '@/components/button-component.vue';
import cityInput from '@/components/inputCity-component.vue';
  export default{
    components:{searchButton, cityInput},
    data(){
      return{
        userInput: "",
        description: "",
        day: "",
        temperature: "",
        wind: "",
        forecast1: "",
        forecast2: "",
        forecast3: "",
      }
    },
    beforeMount(){
      const apiSearch = this.userInput = this.$route.params.id;
      fetch(`https://goweather.herokuapp.com/weather/${apiSearch}`).then(result => result.json())
      .then(value => {
        console.log(value)
        this.description = value.description;
        this.temperature = value.temperature;
        this.forecast1 = value.forecast[0].temperature;
        this.forecast2 = value.forecast[1].temperature;
        this.forecast3 = value.forecast[2].temperature;
      })
      const date = new Date;
      this.day = date.toLocaleDateString('en-US', { weekday: 'long' }) + ' ' +  date.getDate();   
    } 
  }
</script>
<style lang="scss">
@use '@/assets/global-mixins.scss';
  .align-column{
    @include global-mixins.clamp(300px, 100%, 1400px, 700px, 100%, 900px, transparent);
    @include global-mixins.positionDisplay(); 
    padding: 0%;
    margin: auto;
  }
  .weather-card{
    @include global-mixins.heightAndWidth(25%, 85%, #FF9F1C);
    @include global-mixins.positionDisplay(space-evenly, row, center);
    box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
    margin: 1% 0%;
    padding: 3% 1%;
    border-radius: 7px;
  }
  .icon-description{
    @include global-mixins.heightAndWidth(100%, 35%, transparent);
    @include global-mixins.positionDisplay(center, column, center);
    margin: 0% 5%;
    text-align: center;
  }
  .sunny-icon{
    @include global-mixins.heightAndWidth(7rem, 7rem, transparent);
    @include global-mixins.backgroundimg(url('@/assets/icons/sun.png'), 100% 100%);
  }
  .temp-and-wind{
    @include global-mixins.positionDisplay(space-evenly, column, flex-start);
    @include global-mixins.heightAndWidth(100%, 70%, transparent);
    margin: 0% 5%;
    text-align: left;
  }
  .temp-input{
    @include global-mixins.heightAndWidth(10%, 88%, transparent);
    @include global-mixins.positionDisplay(center, row, center);
  }
  .adjust-button{
    position: relative;
    right: 1%;
  }
  .forecasts{
    @include global-mixins.heightAndWidth(45%, 87%, #23395B);
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    align-items: center;
    box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
    border-radius: 7px;
  }
  .grid-childs{
    justify-self: center;
    text-align: center;
    @include global-mixins.positionDisplay(space-evenly, column, center);
    gap: 3%;
  }
  @media screen and (max-width: 1023px) {
    .forecasts{
      grid-template-rows: repeat(3, 1fr);
      grid-template-columns: repeat(2, 1fr);
    }
    .grid-childs{
      @include global-mixins.heightAndWidth(100%, 90%, transparent);
      @include global-mixins.positionDisplay(space-evenly, row, center);
      padding: 2%;
      grid-column: 1/3;
    }
    .child2{
      grid-row: 2;
    }
    .child3{
      grid-row: 3;
    }
    .sunny-icon{
      @include global-mixins.heightAndWidth(4rem, 4rem, transparent);
    }
    .h3-white-styling{
      @include global-mixins.fontStyling(600, #FEFCFB, 24px);
    }
    .h2-white-styling{
      @include global-mixins.fontStyling(600, #FEFCFB, 30px);
    }
    .h4-white-styling{
      @include global-mixins.fontStyling(500, #FEFCFB, 24px);
    }
  }
</style>