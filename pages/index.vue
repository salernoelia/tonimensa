<template>
  <div>
    <h1>Mensa</h1>
    <div class="container">
      <div class="card" v-if="simplyGood">
        <h2>
          Simply Good,
          {{ simplyGood.data.pageProps.recipe?.prices[0].amount }} CHF
        </h2>
        <img
          :src="simplyGood.data.pageProps.recipe?.imageUrl"
          alt="Git leider keis bildli ;)"
          class="image"
        />
        <p>{{ simplyGood.data.pageProps.recipe?.title }}</p>
      </div>

      <div class="card" v-if="daily">
        <h2>Daily, {{ daily.data.pageProps.recipe?.prices[0].amount }} CHF</h2>
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
        <h2>Toni 1, {{ toni1.data.pageProps.recipe?.prices[0].amount }} CHF</h2>
        <img
          :src="toni1.data.pageProps.recipe?.imageUrl"
          alt="Git leider keis bildli ;)"
          class="image"
        />
        <p>{{ toni1.data.pageProps.recipe?.title }}</p>
      </div>
      <div class="card" v-if="toni2">
        <h2>Toni 2, {{ toni2.data.pageProps.recipe?.prices[0].amount }} CHF</h2>
        <img
          :src="toni2.data.pageProps.recipe?.imageUrl"
          alt="Git leider keis bildli ;)"
          class="image"
        />
        <p>{{ toni2.data.pageProps.recipe?.title }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
const date = new Date();
const dateFormat = date.toISOString().split("T")[0];

let simplyGood = ref(null);
let daily = ref(null);
let exquisit = ref(null);

let toni1 = ref(null);
let toni2 = ref(null);

simplyGood.value = await useFetch(
  `https://app.food2050.ch/_next/data/0ZbjvT3bFOuCPDTE2D-jm/de/toni-areal/mensa/food-profile/2024-04-16-mittagsverpflegung-simply-good.json?locationSlug=toni-areal&kitchenSlug=mensa&slug=${dateFormat}-mittagsverpflegung-simply-good`
);

daily.value = await useFetch(
  `https://app.food2050.ch/_next/data/0ZbjvT3bFOuCPDTE2D-jm/de/toni-areal/mensa/food-profile/2024-04-16-mittagsverpflegung-daily.json?locationSlug=toni-areal&kitchenSlug=mensa&slug=${dateFormat}-mittagsverpflegung-daily`
);

exquisit.value = await useFetch(
  `https://app.food2050.ch/_next/data/0ZbjvT3bFOuCPDTE2D-jm/de/toni-areal/mensa/food-profile/2024-04-16-mittagsverpflegung-exquisit.json?locationSlug=toni-areal&kitchenSlug=mensa&slug=${dateFormat}-mittagsverpflegung-exquisit`
);

toni1.value = await useFetch(
  `https://app.food2050.ch/_next/data/0ZbjvT3bFOuCPDTE2D-jm/de/toni-areal/chez-toni/food-profile/2024-04-15-mittagsverpflegung-toni-1.json?locationSlug=toni-areal&kitchenSlug=chez-toni&slug=${dateFormat}-mittagsverpflegung-toni-1`
);
toni2.value = await useFetch(
  `https://app.food2050.ch/_next/data/0ZbjvT3bFOuCPDTE2D-jm/de/toni-areal/chez-toni/food-profile/2024-04-15-mittagsverpflegung-toni-2.json?locationSlug=toni-areal&kitchenSlug=chez-toni&slug=${dateFormat}-mittagsverpflegung-toni-2`
);
</script>

<style scoped>
* {
  font-family: Arial, sans-serif;
}

.image {
  width: 100%;
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
</style>
