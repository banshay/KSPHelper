<template>
  <div class="dropdown">

    <select class="select" v-model="selectedPlanet">
      <option>Planet</option>
      <option v-for="item in kerbol.Planets">{{ item.name }}</option>
    </select>
  </div>
  <div class="dropdown">
    <select class="select">
      <option>Moon</option>
      <option v-for="moon in moons">{{ moon.name }}</option>
    </select>
  </div>
</template>

<script setup lang="ts">

import type {CelestialBody} from "@/stores/kerbol"
import {useKerbolStore} from "@/stores/kerbol";
import {computed, ref} from "vue";

const kerbol = useKerbolStore()
const selectedPlanet = ref("Planet")
const moons = computed((): Record<string, CelestialBody> => {
  return kerbol.Planets[selectedPlanet.value]?.moons ?? {}
})
</script>
