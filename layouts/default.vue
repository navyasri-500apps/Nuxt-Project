<template>
  <div>
    <header class="shadow-sm bg-white">
      <nav class="container mx-auto p-4 flex justify-between">
        <NuxtLink to="/">Home</NuxtLink>
        <NuxtLink to="/email">Email Template</NuxtLink>
        <NuxtLink to="/website">Websites</NuxtLink>
      </nav>
    </header>
    <div>
      <slot />
    </div>
  </div>
</template>

<script setup></script>

<style scoped></style>
