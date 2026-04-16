<script setup lang="ts">
import { RouterView } from 'vue-router';
import 'vue-sonner/style.css'
import { Toaster as SonnerToaster } from '@/components/ui/sonner'

</script>

<template>
  <main>
    <RouterView />
    <SonnerToaster />
  </main>
</template>
