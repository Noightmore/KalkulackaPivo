<script setup>
import Calk from './components/Kalkulacka.vue'
import Footer from "@/components/Footer.vue";

</script>

<template>
    <header>
        <img alt="pivo" class="logo" src="./assets/beer.png" width="527" height="380" />
    </header>

    <main>
        <Calk/>
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

  body {
      width: 100%;
  }


}
</style>
