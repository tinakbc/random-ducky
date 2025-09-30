<script setup>
import { ref } from 'vue' 

const placeholderText = "Because life is better with random ducks."

const duckImg = ref(null)
const error = ref(null)

const fetchDuck = async() => {
 error.value = null

 try {
   const response = await fetch('https://random-d.uk/api/v2/random')
   if (!response.ok) throw new Error('Network response was not ok')
   const data = await response.json()
   duckImg.value = data.url
 }
 catch (err) {
   error.value = 'Quack! Something went wrong.'
 }
}



</script>

<template>
  <header>
    <h1>Unleash the Ducks!</h1>
  </header>

  <main>
    <div>
      <div v-if="duckImg">
        <img :src="duckImg" />
      </div>
    <p v-else>{{ placeholderText }}</p>
    </div>
    <p v-if="error" role="alert">{{ error }}</p>

    <button type="button" @click="fetchDuck">Show me the duck!</button>

  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
