<script lang="ts" setup>
import { Button } from '@/components/ui/button'
</script>

<template>

<div class="bg-[#ffbef3] min-h-screen text-center flex flex-col items-center justify-center">

  <div>
	<img 
		class="w-auto h-100"
		src="/imagines/ghibli/LogoGhibli.png" alt="">
  </div>

	<h1 class="text-xl mt-10 font-medium text-black">
		Discover the magical world of Studio Ghibli
	</h1>

	<p class="text-black">
		An unofficial fan project inspired by Studio Ghibli films
	</p>

  <div class="mt-8 flex gap-5">

    <Button variant="ghibli_btn">
      <RouterLink to="/">
        Exit
      </RouterLink>
    </Button>

    <Button variant="ghibli_btn">
      <RouterLink to="/ghibli/about">
        Enter
      </RouterLink>
    </Button>

  </div>

</div>

</template>