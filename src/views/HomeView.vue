<script setup>
import { ref, onMounted } from 'vue'

const data = ref(null)
const error = ref(null)

onMounted(() => {
  let restUrl = 'https://restcountries.com/v3.1/all';



  fetch(restUrl)
    .then((res) => res.json())
    .then((json) => {
      data.value = json

      console.log('DATA', data.value)
    })
    .catch((err) => (error.value = err))
  })


</script>

<template>
  <main>
    <div class="home">
      
      <div 
        v-if="data && data.length" 
        class="countries"
      >
        <div 
          v-for="countryData in data" 
          :key="countryData.name.common"
          class="countries__item country"
        >
          <RouterLink :to="'/'+countryData.cca3" class="country__flag">
            <img :src="countryData.flags.svg" :alt="countryData.name.common">
          </RouterLink>
          
          <div class="country__details">
            <h2 class="country__name">
              {{ countryData.name.common }}
            </h2>
            <div class="country__row">
              <span>Population</span>: {{ new Intl.NumberFormat('en-EN', {}).format(countryData.population) }}
            </div>
            <div class="country__row">
              <span>Region</span>: {{ countryData.region }}
            </div>
            <div v-if="countryData.capital && countryData.capital.length" class="country__row">
              <span>Capital</span>: {{ countryData.capital[0] }}
            </div>
          </div>
        </div>
      </div>

    </div>
  </main>
</template>

<style scoped>
.countries {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  gap: 48px;
}
.countries__item {

}
.country {
  display: block;
}
.country__flag {
  display: block;
  height: 200px;
  overflow: hidden;
}
.country__flag img {
  display: block;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.country__details {
  padding: 16px;
  margin: 0;
  background: var(--color-background-soft);
  color: var(--vt-c-white);
}

.country__name {
  font-size: 20px;
  font-weight: 800;
  margin-bottom: 12px;
}

.country__row span {
  font-weight: 800;
}
</style>