<template>
  <div class="parent">
    <div></div>
    <div class="child">
      <div class="title">
        <p>{{ dateFormat }} {{ weekDayName }}</p>
      </div>

      <FsLightbox :toggler="toggler" :sources="source" />

      <div v-if="isWeekend == false">
        <h1 class="title">Mensa</h1>
        <div class="container">
          <div class="card" v-if="daily">
            <h2>
              Daily, {{ daily.data.pageProps.recipe?.prices[0].amount }} CHF
            </h2>

            <p>
              Vegetarian: {{ daily.data.pageProps.recipe?.isVegetarian }}
              <br />
              Vegan: {{ daily.data.pageProps.recipe?.isVegan }}
            </p>
            <img
              :src="'daily.data.pageProps.recipe?.imageUrl'"
              alt="Keis Bild :) keis bildli ;)"
              class="image"
              @click="source = ['daily.data.pageProps.recipe?.imageUrl']"
              ;
              toggler="!toggler"
            />
            <h3>{{ daily.data.pageProps.recipe?.title }}</h3>
          </div>

          <div class="card" v-if="simplyGood">
            <h2>
              Simply Good,
              {{ simplyGood.data.pageProps.recipe?.prices[0].amount }} CHF
            </h2>
            <p>
              Vegetarian: {{ simplyGood.data.pageProps.recipe?.isVegetarian }}
              <br />
              Vegan: {{ simplyGood.data.pageProps.recipe?.isVegan }}
            </p>
            <img
              :src="simplyGood.data.pageProps.recipe?.imageUrl"
              alt="Keis Bild :) keis bildli ;)"
              class="image"
              @click="source = [simplyGood.data.pageProps.recipe?.imageUrl]"
              ;
              toggler="!toggler"
            />
            <h3>{{ simplyGood.data.pageProps.recipe?.title }}</h3>
          </div>

          <div class="card" v-if="exquisit">
            <h2>
              Exquisit,
              {{ exquisit.data.pageProps.recipe?.prices[0].amount }} CHF
            </h2>

            <p>
              Vegetarian: {{ exquisit.data.pageProps.recipe?.isVegetarian }}
              <br />
              Vegan: {{ exquisit.data.pageProps.recipe?.isVegan }}
            </p>
            <img
              :src="exquisit.data.pageProps.recipe?.imageUrl"
              alt="Keis Bild :) keis bildli ;)"
              class="image"
              @click="source = [exquisit.data.pageProps.recipe?.imageUrl]"
              ;
              toggler="!toggler"
            />
            <h3>{{ exquisit.data.pageProps.recipe?.title }}</h3>
          </div>
        </div>

        <h1 class="title">Chez</h1>
        <div class="container">
          <div class="card" v-if="toni1">
            <h2>
              Toni 1, {{ toni1.data.pageProps.recipe?.prices[0].amount }} CHF
            </h2>
            <p>
              Vegetarian: {{ toni1.data.pageProps.recipe?.isVegetarian }}
              <br />
              Vegan: {{ toni1.data.pageProps.recipe?.isVegan }}
            </p>
            <img
              :src="toni1.data.pageProps.recipe?.imageUrl"
              alt="Keis Bild :) keis bildli ;)"
              class="image"
              @click="source = [toni1.data.pageProps.recipe?.imageUrl]"
              ;
              toggler="!toggler"
            />
            <h3>{{ toni1.data.pageProps.recipe?.title }}</h3>
          </div>
          <div class="card" v-if="toni2">
            <h2>
              Toni 2, {{ toni2.data.pageProps.recipe?.prices[0].amount }} CHF
            </h2>
            <p>
              Vegetarian: {{ toni2.data.pageProps.recipe?.isVegetarian }}
              <br />
              Vegan: {{ toni2.data.pageProps.recipe?.isVegan }}
            </p>
            <img
              :src="toni2.data.pageProps.recipe?.imageUrl"
              alt="Keis Bild :) keis bildli ;)"
              class="image"
              @click="source = [toni2.data.pageProps.recipe?.imageUrl]"
              ;
              toggler="!toggler"
            />
            <h3>{{ toni2.data.pageProps.recipe?.title }}</h3>
          </div>
        </div>
      </div>

      <div v-else>
        <!-- Random Gif -->
        <img
          :src="randomWoof.data?.url"
          alt="Random Dog could not be resolved :("
          class="image"
        />
        <p>Kein Mensaangebot am Wochenende</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import FsLightbox from "fslightbox-vue/v3";

const toggler = ref(false);
const source = ref < String > "";

const date = new Date();
const dateFormat = date.toISOString().split("T")[0];

let simplyGood = ref(null);
let daily = ref(null);
let exquisit = ref(null);

let isWeekend = ref(date.getDay() === 0 || date.getDay() === 6);
let weekDay = ref(date.getDay());
let weekDayName = ref(date.toLocaleDateString("de-CH", { weekday: "long" }));
// let isWeekend = ref(false);

// let dateFormat = "2024-04-19";

let toni1 = ref(null);
let toni2 = ref(null);

simplyGood.value = await useFetch(
  `https://app.food2050.ch/_next/data/0ZbjvT3bFOuCPDTE2D-jm/de/toni-areal/mensa/food-profile/${dateFormat}-mittagsverpflegung-simply-good.json?locationSlug=toni-areal&kitchenSlug=mensa&slug=${dateFormat}-mittagsverpflegung-simply-good`
);

daily.value = await useFetch(
  `https://app.food2050.ch/_next/data/0ZbjvT3bFOuCPDTE2D-jm/de/toni-areal/mensa/food-profile/${dateFormat}-mittagsverpflegung-daily.json?locationSlug=toni-areal&kitchenSlug=mensa&slug=${dateFormat}-mittagsverpflegung-daily`
);

exquisit.value = await useFetch(
  `https://app.food2050.ch/_next/data/0ZbjvT3bFOuCPDTE2D-jm/de/toni-areal/mensa/food-profile/${dateFormat}-mittagsverpflegung-exquisit.json?locationSlug=toni-areal&kitchenSlug=mensa&slug=${dateFormat}-mittagsverpflegung-exquisit`
);

toni1.value = await useFetch(
  `https://app.food2050.ch/_next/data/0ZbjvT3bFOuCPDTE2D-jm/de/toni-areal/chez-toni/food-profile/${dateFormat}-mittagsverpflegung-toni-1.json?locationSlug=toni-areal&kitchenSlug=chez-toni&slug=${dateFormat}-mittagsverpflegung-toni-1`
);
toni2.value = await useFetch(
  `https://app.food2050.ch/_next/data/0ZbjvT3bFOuCPDTE2D-jm/de/toni-areal/chez-toni/food-profile/${dateFormat}-mittagsverpflegung-toni-2.json?locationSlug=toni-areal&kitchenSlug=chez-toni&slug=${dateFormat}-mittagsverpflegung-toni-2`
);

let randomWoof = ref(null);

randomWoof.value = await useFetch(" https://random.dog/woof.json");
</script>

<style lang="scss" scoped>
@import url("https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,100;0,300;0,400;0,700;0,900;1,100;1,300;1,400;1,700;1,900&display=swap");
* {
  font-family: "Lato", sans-serif;
  font-weight: 100;
  font-style: normal;
}

h1 {
  font-weight: 200;
}

h2 {
  font-weight: 400;
}

h3 {
  font-weight: 300;
}

p {
  font-weight: 300;
}

body {
  overflow: hidden;
}

.parent {
  display: flex;
  position: absolute;
  inset: 0;
}

.child {
  display: flex;
  flex-direction: column;
  color: rgb(0, 0, 0);
  padding: 20px;
  overflow-y: scroll;
  width: 100%;
}

.image {
  width: 300px;
  height: auto;

  margin-bottom: 10px;
}

.card {
  display: flex;
  flex-direction: column;
  padding: 20px;
  width: 350px;
  height: 400px;
  justify-content: center;
  align-items: center;

  background-color: white;
  border: 1px solid #ccc;
  border-radius: 20px;
  transition: all 0.3s ease;

  &:hover {
    box-shadow: 5px 5px 1px 0 rgba(0, 0, 0, 5);
  }
  transition: all 0.3s ease;

  &:hover {
    box-shadow: 5px 5px 1px 0 rgba(0, 0, 0, 5);
  }
}

.container {
  display: flex;
  align-items: start;
  gap: 20px;
  flex-wrap: wrap;
  width: 100%;
  justify-content: start;
}

.allergenes {
  margin: 0;
  padding: 0;
  line-height: 0;
  display: flex;
  flex-wrap: wrap;

  p {
    margin: 0;
    padding: 0;
    line-height: 1;
  }
}
</style>
