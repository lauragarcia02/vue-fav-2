<script lang="ts" setup>

import { computed, ref, watch } from 'vue'
import { useRouter, useRoute } from 'vue-router'
import { films, type Film } from './data'

import { CheckIcon, ChevronsUpDownIcon } from 'lucide-vue-next'

import { cn } from '@/lib/utils'

import { Button } from '@/components/ui/button'

import {
  Command,
  CommandEmpty,
  CommandGroup,
  CommandInput,
  CommandItem,
  CommandList,
} from '@/components/ui/command'

import {
  Popover,
  PopoverContent,
  PopoverTrigger,
} from '@/components/ui/popover'

const route = useRoute()
const router = useRouter()

const film = ref<Film | undefined>(
  films.find(film => film.id === Number(route.params.id))
)

const ghibliFilms = films.map(film => ({
  value: film.id.toString(),
  label: film.title
}))

const open = ref(false)

const value = ref(route.params.id?.toString() || '')

watch(() => route.params.id, (newId) => {

  film.value = films.find(
    film => film.id === Number(newId)
  )

  value.value = newId?.toString() || ''
})

const selectFilm = (filmId: string) => {

  value.value = filmId

  open.value = false

  router.push(`/ghibli/gallery/${filmId}`)
}

const selectedLabel = computed(() => {

  if (!value.value) {
    return 'Select a film...'
  }

  return ghibliFilms.find(
    film => film.value === value.value
  )?.label || 'Select a film...'
})

</script>

<template>

<div
  v-if="film"
  class="w-full max-w-350 md:mx-auto my-8 px-5 md:px-20"
>

  <div class="mb-8 flex flex-row gap-3 items-center justify-end">

    <label class="block text-lg font-semibold text-gray-800">
      Search film:
    </label>

    <Popover v-model:open="open">

      <PopoverTrigger as-child>

        <Button
          variant="outline"
          role="combobox"
          :aria-expanded="open"
          class="w-55 justify-between hover:bg-[#d16bbe] bg-[#ffbef3] border-2 border-black font-semibold hover:text-white shadow-md"
        >
          {{ selectedLabel }}

          <ChevronsUpDownIcon class="ml-2 h-4 w-4 shrink-0 opacity-50" />
        </Button>

      </PopoverTrigger>

      <PopoverContent class="w-55 p-0 border-2 border-black bg-white">

        <Command>

          <CommandInput
            class="border-b-2 border-gray-200"
            placeholder="Search..."
          />

          <CommandList>

            <CommandEmpty>
              Film not found.
            </CommandEmpty>

            <CommandGroup>

              <CommandItem
                v-for="ghibli in ghibliFilms"
                :key="ghibli.value"
                :value="ghibli.value"
                @select="selectFilm(ghibli.value)"
                class="hover:bg-[#d16bbe] hover:text-white cursor-pointer font-medium transition-colors"
              >

                {{ ghibli.label }}

                <CheckIcon
                  :class="cn(
                    'ml-auto',
                    value === ghibli.value
                      ? 'opacity-100'
                      : 'opacity-0'
                  )"
                />

              </CommandItem>

            </CommandGroup>

          </CommandList>

        </Command>

      </PopoverContent>

    </Popover>

  </div>

  <div
    class="flex flex-col lg:flex-row items-start gap-12"
  >

    <figure class="lg:w-1/3 flex justify-center mx-auto">

      <img
        class="h-125 w-auto object-contain"
        :src="`/imagines/ghibli/${film.image}`"
        :alt="film.title"
      />

    </figure>

    <div class="lg:w-2/3 flex flex-col gap-6">

      <h1 class="text-4xl font-bold leading-tight">
        {{ film.title }} | {{ film.original_title }}
      </h1>

      <div class="flex flex-col gap-3 mt-5 text-lg">

        <p>
          <strong>Release date:</strong>
          {{ film.release_date }}
        </p>

        <p>
          <strong>Director:</strong>
          {{ film.director }}
        </p>

        <p>
          <strong>Producer:</strong>
          {{ film.producer }}
        </p>

        <p>
          <strong>Running Time:</strong>
          {{ film.running_time }} min
        </p>

        <p class="mt-8 leading-8 text-justify">
          {{ film.description }}
        </p>

      </div>

    </div>

  </div>

</div>

</template>

<style scoped>
</style>