<script setup lang="ts">
  import { ref } from 'vue';
  import IdsButton from './components/IdsButton.vue'
  // import IdsChip from './components/IdsChip.vue';
  // import { BeakerIcon } from '@heroicons/vue/24/solid'
  // import { MoonIcon } from "@heroicons/vue/24/outline"

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

  type ButtonOptions = {
  mode?: "filled" | "outlined" | "text",
  size?: "compact" | "comfortable" | "spacious",
  variant?: "primary" | "secondary" | "brand" | "error" | "success" | "warning" | "light" | "dark",
  };

  const allModes: Array<ButtonOptions["mode"]> = ["filled", "outlined", "text"];
  const allSizes: Array<ButtonOptions["size"]> = ["compact", "comfortable", "spacious"];
  const allVariants: Array<ButtonOptions["variant"]> = ["primary", "secondary", "brand", "error", "success", "warning", "light", "dark"];

const allOptions: ButtonOptions[] = [];

for (const mode of allModes) {
  for (const size of allSizes) {
    for (const variant of allVariants) {
      const options: ButtonOptions = { mode, size, variant };
      allOptions.push(options);
    }
  }
}
</script>

<template>
  <IdsButton size="comfortable" variant="secondary" @click="drMode" style="margin-bottom: 10px;">{{ darkText }}</IdsButton>
  <!-- <ids-card> -->
  <div class="test">
    <p class="title">Buttons</p>
    <IdsButton v-for="(option, index) in allOptions" :key="index" :size="option.size" :variant="option.variant" :mode="option.mode">
      {{option.mode + ' ' + option.variant + ' ' + option.size}} button
    </IdsButton>
  </div>
  <!-- <div class="test">
    <p class="title">Chips</p>
    <IdsChip >Label</IdsChip>
    <IdsChip >Comfortable Primary</IdsChip>
    <IdsChip size="compact" mode="filled" variant="success">Compact Success</IdsChip>
  </div> -->
<!-- </ids-card> -->
</template>



<style>
@import './styles/ids.scss';
.test {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  margin-bottom: 40px;
}

.title {
  font-size: 20px;
  font-weight: 600;
  margin-bottom: 10px;
}
</style>