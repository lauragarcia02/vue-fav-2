
<script lang="ts" setup>

</script>

<template>
  <div
    class="flex flex-col my-15 lg:flex-row lg:justify-center lg:items-center md:items-center w-full md:mx-auto gap-20 md:px-20"
  >

    <figure class="flex justify-center min-w-min order-2 lg:order-1 h-100">

      <img
        class="object-contain h-full w-auto transition-all duration-300"
        src="/imagines/ghibli/totoro.png"
        alt="Ghibli character"
      />

    </figure>

    <div class="flex flex-col gap-4 order-1 text-center lg:text-left">

      <h1 class=" font-bold text-xl lg:text-5xl mb-5">
        About the Ghibli App
      </h1>

      <div class="lg:max-w-3xl">

        <p class="mb-5">
          Studio Ghibli is one of the most influential animation studios in the world, known for its breathtaking storytelling, emotional depth, and hand-crafted visual style.
        </p>

        <p class="mb-5">
          This app is built as a character gallery where you can explore some of the most iconic characters from Ghibli films, read their descriptions, and navigate through them dynamically.
        </p>

        <p class="mb-5">
          Each character page is generated from a shared dataset, using Vue Router dynamic routes and reusable components to create a smooth and interactive experience.
        </p>

        <p class="mb-5">
          Images used in this project belong to their respective studios and are used here for educational/demo purposes only.
        </p>

      </div>

    </div>

  </div>
</template>

<style scoped>
</style>