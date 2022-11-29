<script setup>
    import { ref, onMounted } from 'vue'
    import { useRoute } from 'vue-router'

    const data = ref(null)
    const route = useRoute()

    onMounted(() => {
        let restUrl = `https://restcountries.com/v3.1/alpha/${route.params.cca3}`;

        fetch(restUrl)
            .then((res) => res.json())
            .then((json) => {
                data.value = json

                console.log('DATA 1', data.value)
            })
            .catch((err) => (error.value = err))
    });

</script>

<template>
    <div class="country">
      <h1>This is the full country details</h1>
    </div>
</template>
  
  <style>
  
  </style>
  