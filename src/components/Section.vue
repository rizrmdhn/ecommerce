<template>
  <div v-if="this.items.id > 0 && this.items.id < 20" class="section">
    <div
      v-if="this.items.category === `women's clothing`"
      class="woman-box"
    ></div>
    <div v-else class="blue-box"></div>
    <div class="item-box">
      <img class="item-image" alt="test" :src="this.items.image" />
      <div class="item-content">
        <p
          v-if="this.items.category === `women's clothing`"
          class="woman-item-title"
        >
          {{ this.items.title }}
        </p>
        <p v-else class="item-title">{{ this.items.title }}</p>
        <h5 class="item-type text-muted">
          {{ this.items.category }}
        </h5>
        <div class="line"></div>
        <h5 class="item-desc">{{ this.items.description }}</h5>
        <div class="line"></div>
        <h5
          v-if="this.items.category === `women's clothing`"
          class="woman-price"
        >
          ${{ this.items.price }}
        </h5>
        <h5 v-else class="price">${{ this.items.price }}</h5>
        <div class="item-content__action-button">
          <button
            v-if="this.items.category === `women's clothing`"
            class="woman-buy"
          >
            <p class="">Buy Now</p>
          </button>
          <button v-else class="buy">
            <p class="buy-button">Buy Now</p>
          </button>
          <button
            v-if="this.items.category === `women's clothing`"
            class="woman-next"
            @click="nextProduct"
          >
            <p>Next Product</p>
          </button>
          <button v-else class="next" @click="nextProduct">
            <p>Next Product</p>
          </button>
        </div>
      </div>
    </div>
  </div>
  <div v-else class="unavailable">
    <div class="unavailable-box"></div>
    <div class="unavailable-card">
      <h1 class="unavailable-title">This product is unavailable to show.</h1>
      <button class="unavailable-button">
        <p>Next Product</p>
      </button>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      items: [],
      id: 1,
    };
  },
  mounted() {
    axios.get(`https://fakestoreapi.com/products/${this.id}`).then((res) => {
      const items = res.data;
      this.items = items;
    });
  },
  methods: {
    nextProduct() {
      this.id++;
      axios.get(`https://fakestoreapi.com/products/${this.id}`).then((res) => {
        const items = res.data;
        this.items = items;
      });
    },
  },
};
</script>

<style>
/* universal */
button {
  cursor: pointer;
}

/* for unavailable section */
.unavailable-box {
  height: 640px;
  background: #d8d7d7;
  transition: 500ms;
}
.unavailable-card {
  position: absolute;
  width: 1034px;
  height: 580px;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  background: #ffffff;
  border-radius: 10px;
}
.unavailable-title {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-weight: 400;
  font-size: 20px;
  line-height: 24px;
  color: #000000;
}
.unavailable-button {
  width: 465px;
  height: 42px;
  position: absolute;
  top: 55%;
  left: 50%;
  transform: translate(-50%, -30%);
  background: #ffffff;
  border: 3px solid #000000;
  border-radius: 4px;
}
.unavailable-button > p {
  font-weight: 600;
  font-size: 20px;
  line-height: 24px;
  color: #3f3f3f;
}
/* for men section */
.blue-box {
  height: 640px;
  background-color: #d6e6ff;
  transition: 500ms;
}
.item-box {
  width: 1450px;
  height: 750px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  border-radius: 10px;
  background-color: #ffffff;
}
.item-image {
  width: 351px;
  height: 453px;
  margin: auto;
  margin-top: 150px;
  margin-left: 150px;
}
.item-content {
  position: absolute;
  width: 700px !important;
  height: 645px !important;
  top: 50%;
  left: 75%;
  transform: translate(-60%, -50%);
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  border-radius: 10px;
  background-color: #ffffff;
}
.item-title {
  margin: 15px 45px;
  font-weight: 600;
  font-size: 28px;
  line-height: 34px;
  color: #002772;
}
.item-type {
  margin: 15px 45px;
  font-weight: 400;
  font-size: 18px;
  line-height: 22px;
}
.line {
  margin: 15px 45px;
  width: 585px;
  border: 1px solid rgba(0, 0, 0, 0.2);
}
.price {
  margin: 15px 45px;
  font-weight: 600;
  font-size: 28px;
  height: 38px;
  color: #002772;
}
.item-desc {
  margin: 15px 45px;
  width: 538px;
  height: 330px;
  font-weight: 300;
  font-size: 20px;
  line-height: 23px;
  color: #1e1e1e;
}
img {
  position: relative;
  width: 301px;
  height: 383px;
}
.buy {
  margin: auto;
  margin-left: 130px;
  margin-right: 45px;
  width: 200px;
  height: 38px;
  background: #002772;
  border-radius: 4px;
}
.buy > p {
  font-size: 20px;
  font-weight: 600;
  color: #ffffff;
}
.next {
  width: 200px;
  height: 38px;
  background: #ffffff;
  border: 3px solid #002772;
  border-radius: 4px;
}
.next > P {
  font-size: 20px;
  font-weight: 600;
  color: #002772;
}

/* for women section */

.woman-box {
  height: 640px;
  background: #fde2ff;
}
.woman-item-title {
  margin: 15px 45px;
  font-weight: 600;
  font-size: 28px;
  line-height: 34px;
  color: #720060;
}
.woman-price {
  margin: 15px 45px;
  font-weight: 600;
  font-size: 28px;
  height: 38px;
  color: #720060;
}
.woman-buy {
  margin: auto;
  margin-left: 130px;
  margin-right: 45px;
  width: 200px;
  height: 38px;
  background: #720060;
  border-radius: 4px;
}
.woman-buy > p {
  font-size: 20px;
  font-weight: 600;
  color: #ffffff;
}
.woman-next {
  width: 200px;
  height: 38px;
  background: #ffffff;
  border: 3px solid #720060;
  border-radius: 4px;
}
.woman-next > P {
  font-family: "Inter";
  font-style: normal;
  font-weight: 600;
  font-size: 20px;
  line-height: 24px;

  color: #720060;
}
</style>
