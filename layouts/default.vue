<script setup lang="ts"></script>

<template>
  <div>
    <ul class="flex">
      <li class="mr-6">
        <NuxtLink class="text-blue-500" to="/">Home</NuxtLink>
      </li>
      <li class="mr-6">
        <NuxtLink class="text-blue-500" to="/auth">Auth</NuxtLink>
      </li>
      <li class="mr-6">
        <NuxtLink class="text-blue-500" to="/guest">Guest</NuxtLink>
      </li>
      <li class="mr-6">
        <NuxtLink class="text-blue-500" to="/login">Login</NuxtLink>
      </li>
      <li class="mr-6">
        <NuxtLink class="text-blue-500" to="/register">Register</NuxtLink>
      </li>
    </ul>
    <slot />
  </div>
</template>