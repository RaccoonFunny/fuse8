<template>
  <div id="app">
    <h1>Our Latest Developments</h1>
    <label>
      <span>Filter</span>
      <input type="text" v-model="filter">
    </label>
    <div class="houses">
      <house-card v-for="house in houses[page]" :house="house" :key="house.id"/>
    </div>
    <button class="see-more">
      See more
      <svg width="7" height="17" viewBox="0 0 7 17" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M1 1L5.043 8.41667L1 15.8333" stroke="#363636" stroke-width="2" stroke-linecap="round"/>
      </svg>
    </button>
  </div>
</template>

<script>
import HouseCard from "@/components/HouseCard";

export default {
  name: 'App',
  components: {HouseCard},
  data: function () {
    return {
      filter: "",
      houses: [],
      page: 0,
      apiData: [],
      scrollWidth: 0,
      blockInScreen: 1,
    }
  },
  watch: {
    filter: function () {
      let filter = [];
      this.houses = [];
      for (let i = 0; i < this.apiData.length; i++) {
        if (this.apiData[i].title.toLowerCase().indexOf(this.filter.toLowerCase()) !== -1){
          filter.push(this.apiData[i]);
        }
      }
      for (let i = 0; i < filter.length; i += this.blockInScreen) {
        this.houses.push(filter.slice(i, i + this.blockInScreen));
      }
    }
  },
  beforeMount() {
    let requestOptions = {
      method: 'GET',
      redirect: 'follow'
    };

    //узнаём примерную ширину доступного пространства без учёта полосы прокрутки браузера
    this.scrollWidth = Math.max(
        document.body.scrollWidth, document.documentElement.scrollWidth,
        document.body.scrollWidth, document.documentElement.scrollWidth,
        document.body.scrollWidth, document.documentElement.scrollWidth
    );

    this.blockInScreen = 2 * Math.floor(this.scrollWidth / 403);

    fetch("https://603e38c548171b0017b2ecf7.mockapi.io/homes", requestOptions)
        .then(response => response.text())
        .then(result => {
          result = JSON.parse(result);
          this.apiData = result;
          for (let i = 0; i < result.length; i += this.blockInScreen) {
            this.houses.push(result.slice(i, i + this.blockInScreen));
          }
        })
        .catch(error => console.log('error', error));
  },
  mounted() {
  }
}
</script>

<style lang="scss">
@import "./variable.scss";
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@300;400;600;700;800&display=swap');

* {
  margin: 0;
  padding: 0;
  font-family: "Open Sans", sans-serif;
  font-style: normal;
}

#app {
  margin: 0 50px;

  h1 {
    margin: 36px 0 43px 0;
    font-weight: bold;
    font-size: 36px;
    line-height: 49px;
    text-align: center;
    color: #45852D;
  }

  label {
    font-style: normal;
    font-weight: bold;
    font-size: 16px;
    line-height: 24px;
    letter-spacing: -0.3px;
    color: $black;

    span {
      margin-right: 15px;
    }

    input {
      border: 1px solid $white;
      box-sizing: border-box;
      border-radius: 25px;
      width: 418px;
      padding: 16px;
      margin-bottom: 45px;
    }
  }

  .houses {
    display: grid;
    grid-gap: 38px 22px;
    grid-template-columns: repeat(auto-fill, 381px);
  }

  .see-more {
    margin: 60px auto;
    display: flex;
    padding: 12px 33px 14px 33px;
    align-items: center;
    gap: 10px;
    font-style: normal;
    font-weight: bold;
    font-size: 16px;
    line-height: 24px;
    letter-spacing: -0.3px;
    color: $black;
    border: 1px solid $white;
    border-radius: 25px;
    background: white;
    cursor: pointer;
  }

}
</style>
