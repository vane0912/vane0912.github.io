<template>
  <div class="input-button">
    <div class="wrap-in-li">
      <input class="input-styling" ref="inputValue" type="text" v-model="city">
      <div ref="toggleDisplay" v-if="show" class="allCities">
        <ul style="list-style-type: none; padding: 0;" ref="dontDisplay" @click="setInputValue($event)">
          <li v-for="cities in filterCity">{{ cities }}</li>
        </ul>
      </div>
    </div>
      <button @click="searchCountry()" class="button-styling">Search</button>
  </div>
</template>
<script >
export default{
    data(){
        return{
            citiesApi: [],
            city: "",
            show: false
        }
    },
    watch:{
      city(txt){
        return txt.length > 0 ? this.show = true : this.show = false;
      }
    },
    computed:{
    filterCity(){
      fetch('https://countriesnow.space/api/v0.1/countries')
      .then(response => response.json()).then(data => this.citiesApi = data.data)
      const toLc = this.citiesApi.map(values => values.cities).flat(1);
      return toLc.filter(values => values.toLowerCase().includes(this.city.toLowerCase()))
    }
  },
  methods:{
    searchCountry(){
      const userCity = this.city;
      this.$route.params.id = userCity;
      this.$router.push({name:'about'})
    },
    setInputValue(click){
      this.$refs.toggleDisplay.classList.toggle("display-none");
      const targetValue = click.target.textContent
      this.city = targetValue;
    }
  }
}
</script>
<style lang="scss">
@use '@/assets/global-mixins.scss';
.input-styling{
    @include global-mixins.minMax(100%, 60rem, 97%, 10rem);
    @include global-mixins.fontStyling(200, #F0F7F4, 20px);
    border-radius: 5px;
    border: none;
    text-align: center;
      & .input-styling:focus{
        outline: #F0F7F4;
      }
}
.wrap-in-li{
  @include global-mixins.heightAndWidth(100%, 100%, transparent)
}
.filter{
    display: flex;
    flex-direction: column;
    @include global-mixins.heightAndWidth(100%, 100%, transparent)
}
.button-styling{
    @include global-mixins.minMax(60%, 20rem, 100%, 10rem, #70ABAF);
    @include global-mixins.fontStyling(100, #F0F7F4, 20px);
    border-radius: 5px;
    border: solid 1px #23395B;
    position: relative;
    right: 1%;
    cursor: pointer;
}
.input-button{
    @include global-mixins.minMax(100%, 100%, 100%, 4rem, transparent);
    @include global-mixins.positionDisplay(flex-start, row, center);
} 
.allCities{
  @include global-mixins.fontStyling(100, #F0F7F4, 20px);
  @include global-mixins.heightAndWidth(auto, 100%, #23395B);
  z-index: 1;
  max-height: 10rem;
  border-radius: 3px;
  overflow: scroll;
}
.allCities li{
  cursor: pointer;
  padding: 2%;
  &:hover{
    background-color: #2a456c;
  }
}
.display-none{
  display: none;
}
</style>