<script lang="ts" setup>
import Button from '@/components/ui/button/Button.vue'
</script>

<template>

<div class="grid grid-rows-[auto_1fr_auto] min-h-screen">

  <header class="bg-[#ffbef3] w-full border border-black">

    <div class="flex flex-col md:flex-row items-center justify-between p-5 mx-auto max-w-350 md:px-20">

      <img 
        src="/imagines/ghibli/LogoGhibli.png" alt=""
        class="w-auto h-15">

      <div class="flex justify-center items-center gap-6 pt-3 text-white">

        <RouterLink to="/ghibli/gallery" class="text-black" active-class="font-bold">
          Films
        </RouterLink>

        <RouterLink to="/ghibli/about" class="text-black" active-class="font-bold">
          About
        </RouterLink>

        <Button
          variant="ghibli_btn"
        >
          <RouterLink to="/ghibli">
            Exit
          </RouterLink>
        </Button>

      </div>

    </div>

  </header>

  <main>
    <RouterView />
  </main>

  <footer class="text-center bg-[#ffbef3] w-full border border-black py-6 text-black">

    <div>
      <strong>Studio Ghibli Fan Project</strong>
    </div>

    <small>
      Created by Laura García
    </small>

  </footer>

</div>

</template>

<style scoped>
</style>