<template>
  <div>
    <h1>{{ dateFormat }} {{ weekDayName }}</h1>
    <div v-if="isWeekend == false">
      <h1>Mensa</h1>
      <div class="container">
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
            alt="Git leider keis bildli ;)"
            class="image"
          />
          <p>{{ simplyGood.data.pageProps.recipe?.title }}</p>
        </div>

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
            :src="daily.data.pageProps.recipe?.imageUrl"
            alt="Git leider keis bildli ;)"
            class="image"
          />
          <p>{{ daily.data.pageProps.recipe?.title }}</p>
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
            alt="Git leider keis bildli ;)"
            class="image"
          />
          <p>{{ exquisit.data.pageProps.recipe?.title }}</p>
        </div>
      </div>

      <h1>Chez</h1>
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
            alt="Git leider keis bildli ;)"
            class="image"
          />
          <p>{{ toni1.data.pageProps.recipe?.title }}</p>
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
            alt="Git leider keis bildli ;)"
            class="image"
          />
          <p>{{ toni2.data.pageProps.recipe?.title }}</p>
        </div>
      </div>
    </div>

    <div v-else>
      <!-- Random Gif -->
      <img :src="randomWoof.data?.url" alt="randomWoof" class="image" />
      <p>Kein Mensaangebot am Wochenende</p>
    </div>
  </div>
</template>

<script setup>
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

<style scoped>
* {
  font-family: Arial, sans-serif;
}

.image {
  width: 300px;
  height: auto;
  margin-bottom: 10px;
}

.card {
  margin: 20px;
  padding: 20px;
  width: 300px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.container {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
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
