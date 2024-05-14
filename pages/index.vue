<template>
  <div class="parent">
    <div class="child">
      <p>{{ dateFormat }} {{ weekDayName }}</p>
      <div v-if="!isWeekend">
        <h1 class="title">Mensa</h1>
        <div class="container">
          <div class="card" v-for="(meal, index) in meals" :key="index">
            <h2>
              {{ meal.name }},
              {{ meal.data?.pageProps?.recipe?.prices[0].amount }} CHF
            </h2>

            <p>
              Vegetarian: {{ meal.data?.pageProps?.recipe?.isVegetarian }}
              <br />
              Vegan: {{ meal.data?.pageProps?.recipe?.isVegan }}
            </p>
            <img
              :src="meal.data?.pageProps?.recipe?.imageUrl"
              alt="Git leider keis bildli ;)"
              class="image"
            />
            <h3>{{ meal.data?.pageProps?.recipe?.title }}</h3>
          </div>
        </div>

        <h1 class="title">Chez</h1>
        <div class="container">
          <div class="card" v-for="(meal, index) in chezMeals" :key="index">
            <h2>
              {{ meal.name }},
              {{ meal.data?.pageProps?.recipe?.prices[0].amount }} CHF
            </h2>

            <p>
              Vegetarian: {{ meal.data?.pageProps?.recipe?.isVegetarian }}
              <br />
              Vegan: {{ meal.data?.pageProps?.recipe?.isVegan }}
            </p>
            <img
              :src="meal.data?.pageProps?.recipe?.imageUrl"
              alt="Git leider keis bildli ;)"
              class="image"
            />
            <h3>{{ meal.data?.pageProps?.recipe?.title }}</h3>
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
const date = new Date();
const dateFormat = date.toISOString().split("T")[0];

let isWeekend = ref(date.getDay() === 0 || date.getDay() === 6);
let weekDay = ref(date.getDay());
let weekDayName = ref(date.toLocaleDateString("de-CH", { weekday: "long" }));

let meals = ref([
  { name: "Daily", data: null },
  { name: "Simply Good", data: null },
  { name: "Exquisit", data: null },
]);

let chezMeals = ref([
  { name: "Toni 1", data: null },
  { name: "Toni 2", data: null },
]);

let randomWoof = ref(null);

async function fetchMeals() {
  meals.value[0].data = await useFetch(
    `https://app.food2050.ch/_next/data/EP5SGBYLSzqC8kcQS94Ha/de/toni-areal/mensa/food-profile/${dateFormat}-mittagsverpflegung-daily.json?locationSlug=toni-areal&kitchenSlug=mensa&slug=${dateFormat}-mittagsverpflegung-daily`
  );

  meals.value[1].data = await useFetch(
    `https://app.food2050.ch/_next/data/EP5SGBYLSzqC8kcQS94Ha/de/toni-areal/mensa/food-profile/${dateFormat}-mittagsverpflegung-simply-good.json?locationSlug=toni-areal&kitchenSlug=mensa&slug=${dateFormat}-mittagsverpflegung-simply-good`
  );

  meals.value[2].data = await useFetch(
    `https://app.food2050.ch/_next/data/EP5SGBYLSzqC8kcQS94Ha/de/toni-areal/mensa/food-profile/${dateFormat}-mittagsverpflegung-exquisit.json?locationSlug=toni-areal&kitchenSlug=mensa&slug=${dateFormat}-mittagsverpflegung-exquisit`
  );

  chezMeals.value[0].data = await useFetch(
    `https://app.food2050.ch/_next/data/EP5SGBYLSzqC8kcQS94Ha/de/toni-areal/chez-toni/food-profile/${dateFormat}-mittagsverpflegung-toni-1.json?locationSlug=toni-areal&kitchenSlug=chez-toni&slug=${dateFormat}-mittagsverpflegung-toni-1`
  );

  chezMeals.value[1].data = await useFetch(
    `https://app.food2050.ch/_next/data/EP5SGBYLSzqC8kcQS94Ha/de/toni-areal/chez-toni/food-profile/${dateFormat}-mittagsverpflegung-toni-2.json?locationSlug=toni-areal&kitchenSlug=chez-toni&slug=${dateFormat}-mittagsverpflegung-toni-2`
  );

  randomWoof.value = await useFetch(" https://random.dog/woof.json");
}

fetchMeals();
</script>

<style lang="scss" scoped>
@import url("https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,100;0,300;0,400;0,700;0,900;1,100;1,300;1,400;1,700;1,900&display=swap");
* {
  font-family: Arial, Helvetica, sans-serif;
  font-family: "Lato", sans-serif;
  font-weight: 100;
  font-style: normal;
}

h1 {
  font-weight: 300;
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
  max-height: 450px;
  justify-content: start;
  align-items: start;

  background-color: white;
  border: 1px solid #ccc;
  border-radius: 20px;
  transition: all 0.3s ease;

  &:hover {
    box-shadow: 5px 5px 1px 0 rgba(0, 0, 0, 2);
  }
}

.container {
  display: flex;
  align-items: start;
  gap: 20px;
  flex-wrap: wrap;
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
