<script lang="ts" setup>

import { Card } from '@/components/ui/card'
import CardContent from '@/components/ui/card/CardContent.vue'

import { films } from './data'

import { computed, ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

const inPagina = 3
const nuncPagina = ref(1)

const totalPaginae = computed(() =>
  Math.ceil(films.length / inPagina)
)

const listaGhibli = computed(() => {
  const inicio = (nuncPagina.value - 1) * inPagina
  const fin = inicio + inPagina
  return films.slice(inicio, fin)
})

const ireAdPaginam = (pagina: number) => {
  if (pagina >= 1 && pagina <= totalPaginae.value) {
    nuncPagina.value = pagina
  }
}

const paginaMumeri = computed(() =>
  Array.from({ length: totalPaginae.value }, (_, i) => i + 1)
)

</script>

<template>

<div class="flex flex-col items-center justify-center gap-8 w-full max-w-350 my-8 mx-auto">

  <div class="text-center">

    <h1 class="font-bold text-xl lg:text-5xl mb-5">
      Studio Ghibli Film Gallery
    </h1>

    <p class="mb-5">
      Click on a film to explore it
    </p>

  </div>

  <div class="flex gap-8 px-2">

    <Card
      v-for="film in listaGhibli"
      :key="film.id"
      class="cursor-pointer w-75 h-105 hover:bg-[#ffdff9] transition-all"
    >

      <CardContent
        class="flex flex-col items-center text-center justify-center gap-1 w-full"
        @click="router.push(`/ghibli/gallery/${film.id}`)"
      >

        <img
          :src="`/imagines/ghibli/${film.image}`"
          :alt="film.title"
          class="w-60 h-80 object-cover object-center rounded-md"
        />

        <div class="flex flex-col items-center text-center mt-1">
            <h2 class="font-medium text-lg ">
             {{ film.title }}
            </h2>

            <p>
            {{ film.release_date }}
            </p>
        </div>

        

      </CardContent>

    </Card>

  </div>

  <div class="flex items-center justify-center gap-2 mt-4">

    <button
      @click="ireAdPaginam(nuncPagina - 1)"
      :disabled="nuncPagina === 1"
      :class="[
        'px-4 py-2 rounded-md font-medium transition-colors',
        nuncPagina === 1
          ? 'bg-[#ffecfb] text-[#d16bbe] cursor-not-allowed'
          : 'bg-[#ffbef3] hover:bg-black hover:text-white'
      ]"
    >
      Previous
    </button>

    <button
      v-for="pagina in paginaMumeri"
      :key="pagina"
      @click="ireAdPaginam(pagina)"
      :class="[
        'w-10 h-10 rounded-md font-medium transition-colors',
        nuncPagina === pagina
          ? 'bg-[#d16bbe] text-gray-800'
          : 'bg-[#ffbef3] hover:bg-black hover:text-white'
      ]"
    >
      {{ pagina }}
    </button>

    <button
      @click="ireAdPaginam(nuncPagina + 1)"
      :disabled="nuncPagina === totalPaginae"
      :class="[
        'px-4 py-2 rounded-md font-medium transition-colors',
        nuncPagina === totalPaginae
          ? 'bg-[#ffecfb] hover:bg-black hover:text-white text-[#d16bbe] cursor-not-allowed'
          : 'bg-[#ffbef3] hover:bg-black hover:text-white'
      ]"
    >
      Next
    </button>

  </div>

</div>

</template>

<style scoped>
</style>