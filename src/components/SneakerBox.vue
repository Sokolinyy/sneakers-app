<template lang="">
  <div class="grid-container">
    <h2>Sneaker</h2>
    <ul class="sneakers">
      <li v-for="sneaker in sneakers" :key="sneaker.id">
        <img :src="sneaker.imageUrl.mainImage" alt="" class="sneaker-img" />
        <p class="sneaker-name">
          {{ sneaker.name }}
        </p>
        <p class="sneaker-price">{{ formatPrice(sneaker.price) }} Kč</p>
      </li>
    </ul>
  </div>
</template>
<script lang="ts" setup>
import { ref } from "vue";

interface Sneaker {
  id: number;
  name: string;
  price: number;
  imageUrl: {
    mainImage: string;
    image: string;
    image1: string;
  };
  sizes: number[];
}

const sneakers = ref<Sneaker[]>([]);

const fetchData = async () => {
  const response = await fetch(
    "https://6468f45a03bb12ac2082ccee.mockapi.io/sneakers"
  );
  const data = await response.json();
  console.log(data);
  sneakers.value = data;
};
fetchData();

const formatPrice = (price: number) => {
  return price.toLocaleString("en-US", {
    style: "currency",
    currency: "USD",
    minimumFractionDigits: 2,
  });
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=EB+Garamond:wght@400;500;600;700;800&family=Roboto:wght@400;500;700;900&display=swap");

.grid-container {
  .sneakers {
    width: 100%;
    display: grid;
    grid-template-columns: repeat(
      3,
      1fr
    ); /* Create 3 equal-width columns in each row */
    list-style: none;
    grid-gap: 20px;

    li {
      display: flex;
      flex-direction: column;
      width: calc(69.8% - 20px);
      text-align: left;
      padding-bottom: 40px;
      border-radius: 10px;
      border: 1px solid transparent;

      &:hover {
        background-color: white;
        border: 1px solid black;
      }
    }

    p {
      margin: 10px;
    }

    .sneaker-img {
      width: 300px; /* You can adjust this width as needed */
      border-radius: 10px;
    }

    .sneaker-name {
      font-size: 17px;
      font-weight: 600;
    }

    .sneaker-price {
      margin-top: 40px;
      font-weight: 800;
      font-size: 18px;
    }
  }
}
</style>
