<script setup lang="ts">
const { t } = useI18n()
</script>

<template>
  <nav class=" align-middle text-2xl my-2">
    <a class="">快速导航：</a>
    <router-link class="text-2xl icon-btn mx-2 " to="/" :title="t('button.home')">
      {{ t('button.home') }}
    </router-link>
    <router-link class="text-2xl icon-btn mx-2 " to="/webgl" :title="'webgl'">
      web3D
    </router-link>
    <router-link class="text-2xl icon-btn mx-2" to="/about" :title="t('button.about')">
      {{ t('button.about') }}
    </router-link>
  </nav>
</template>
