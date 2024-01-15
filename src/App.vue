<script setup lang="ts">
  import { ref } from 'vue';
import IdsButton from './components/IdsButton.vue'
  import { ComputerDesktopIcon } from '@heroicons/vue/24/outline';
  const darkText = ref('lightMode');
  function drMode() {
    if (document.documentElement.classList.contains('dark')) {
      document.documentElement.classList.remove('dark')
      darkText.value = 'lightMode';
    } else {
      document.documentElement.classList.add('dark')
      darkText.value = 'darkMode';
    }
  }
</script>

<template>
  <IdsButton size="comfortable" variant="secondary" @click="drMode" style="margin-bottom: 10px;">{{ darkText }}</IdsButton>
  <!-- <ids-card> -->
  <div class="test">
    <IdsButton size="compact" variant="primary" >
      Compact Primary</IdsButton>
    <IdsButton size="comfortable" variant="secondary" >Comfortable Secondary</IdsButton>
    <IdsButton size="spacious" variant="brand" >Spacious Brand</IdsButton>
    <IdsButton size="spacious" variant="error" >Spacious Error</IdsButton>
    <IdsButton size="spacious" variant="success" >
      Spacious Success
      <ComputerDesktopIcon class="w-10px h-10px text-gray-200 cursor-pointer hover:opacity-60" />
    </IdsButton>
    <IdsButton size="spacious" variant="warning" >Spacious Warning</IdsButton>
    <IdsButton mode="outlined" size="spacious" variant="primary" >outline</IdsButton>
    <IdsButton mode="text" size="comfortable" variant="success">text</IdsButton>
  </div>
<!-- </ids-card> -->
</template>

<style>
@import './styles/ids.scss';
.test {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}
</style>