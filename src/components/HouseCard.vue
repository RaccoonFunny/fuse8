<template>
  <div class="card">
    <img src="https://lk.cottage.ru/storage/articles/260/260359/5fccbca8e1468b36c84fc0b39caf219f.jpg?v=1602765804" alt="">
    <div class="type">
      <span v-if="house.type === 'IndependentLiving'" class="independent-living">
        Independent living
      </span>
      <span v-if="house.type !== 'IndependentLiving'" class="restaurant-available">
        Restaurant & Support available
      </span>
    </div>
    <h2 class="title">
      {{ house.title }}
    </h2>
    <p class="address">
      {{ house.address }}
    </p>
    <p class="price">
      New Properties for Sale from
      <strong>
        £{{ house.price }}
      </strong>
    </p>
    <p class="ownership">
      <small>
        Shared Ownership Available
      </small>
    </p>
  </div>
</template>

<script>
export default {
  name: "HouseCard",
  props: {
    house: Object,
  }
}
</script>

<style lang="scss" scoped>
@import "../variable.scss";

.card {
  width: 379px;
  height: 381px;
  background: #f8f8f8;
  border: 1px solid $white;

  img {
    width: 379px;
    height: 233px;
  }

  .title {
    font-weight: bold;
    font-size: 20px;
    line-height: 27px;
    color: $black;
    margin: 20px 0 2px 20px;
  }

  .address {
    margin: 0 0 15px 20px ;
    font-style: normal;
    font-weight: normal;
    font-size: 16px;
    line-height: 22px;
    color: $black;
  }

  .price {
    font-style: normal;
    font-weight: normal;
    font-size: 16px;
    line-height: 22px;
    color: $black;
    margin: 0 0 7px 20px;
  }

  .ownership {
    font-style: normal;
    font-weight: normal;
    font-size: 14px;
    line-height: 19px;
    color: $black;
    margin-left: 20px;
  }
}

.type {
  text-align: end;
  margin: -32px 0 0 0;
}

.independent-living {
  background: #006F79;
  padding: 8px 8px 5px 8px;
  color: #fff;
}

.restaurant-available {
  background: #EC6608;
  padding: 8px 8px 5px 8px;
  color: #fff;
}

</style>
