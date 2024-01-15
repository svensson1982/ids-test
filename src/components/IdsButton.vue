
<script setup lang="ts">
import { reactive } from 'vue';
const props = withDefaults(defineProps<{
  type?: "submit" | "button" | "reset",
  mode?: "filled" | "outlined" | "text",
  size?: "compact" | "comfortable" | "spacious",
  variant?: "primary" | "secondary" | "brand" | "error" | "success" | "warning" | "light" | "dark",
}>(), {
  type: 'button',
  mode: 'filled',
  size: 'comfortable',
  variant: 'primary',
});

const buttonStyle = reactive({
  //enabled
  opacity: `var(--comp-buttons-size-${props.size}-border, 1)`,
  color: `var(--comp-buttons-${props.mode}-color-fg-${props.variant}-enabled)`,
  borderRadius: `var(--comp-buttons-size-${props.size}-border-radius, 1000px)`,
  background: ` var(--comp-buttons-${props.mode}-color-bg-${props.variant}-enabled)`,
  border: `var(--comp-buttons-size-${props.size}-border, 1px) solid var(--comp-buttons-${props.mode}-color-border-${props.variant}-enabled, rgba(255, 255, 255, 0.00))`,
  
  //hovered
  hoverBackground: `var(--comp-buttons-${props.mode}-color-bg-${props.variant}-hovered)`,
  hoverBorder: `var(--comp-buttons-size-${props.size}-border, 1px) solid var(--comp-buttons-${props.mode}-color-border-${props.variant}-hovered, rgba(255, 255, 255, 0.00))`,
  
  //focused
  focusedBackground: `var(--comp-buttons-${props.mode}-color-bg-${props.variant}-focused)`,
  focusedBorder: `var(--comp-buttons-size-${props.size}-border, 1px) solid var(--comp-buttons-${props.mode}-color-border-${props.variant}-focused, rgba(255, 255, 255, 0.00))`,
  
  //disabled
  disabledColor: `var(--comp-buttons-${props.mode}-color-fg-${props.variant}-disabled)`,
  disabledBackground: `var(--comp-buttons-${props.mode}-color-bg-${props.variant}-disabled)`,
  disabledBorder: `var(--comp-buttons-size-${props.size}-border, 1px) solid var(--comp-buttons-${props.mode}-color-border-${props.variant}-disabled, rgba(255, 255, 255, 0.00))`,

  //active
  activeBackground: `var(--comp-buttons-${props.mode}-color-bg-${props.variant}-pressed)`,
  activeBorder: `var(--comp-buttons-size-${props.size}-border, 1px) solid var(--comp-buttons-${props.mode}-color-border-${props.variant}-pressed, rgba(255, 255, 255, 0.00))`,  
  

});

</script>

<template>
  <!-- :class="[size, variant]" -->
  <button :type="type" :class="[size, 'ids-button']">
  <slot></slot>
  </button>
</template>

<style scoped lang="scss">

@mixin common {
  flex-shrink: 0;
  align-items: center;
  display: inline-flex;
  justify-content: center;
}

//sizes
.compact {
  @include common;
  gap: var(--comp-buttons-size-compact-gap, 4px);
  height: var(--comp-buttons-size-compact-height, 24px);
  padding: var(--comp-buttons-size-compact-padding-y, 6px) var(--comp-buttons-size-compact-padding-x, 8px);
}

.comfortable {
  @include common;
  gap: var(--comp-buttons-size-comfortable-gap, 8px);
  height: var(--comp-buttons-size-comfortable-height, 40px);
  padding: var(--comp-buttons-size-comfortable-padding-y, 10px) var(--comp-buttons-size-comfortable-padding-x, 20px);
}

.spacious {
  @include common;
  gap: var(--comp-buttons-size-spacious-gap, 8px);
  height: var(--comp-buttons-size-spacious-height, 56px);
  padding: var(--comp-buttons-size-spacious-padding-y, 16px) var(--comp-buttons-size-spacious-padding-x, 24px);
}

//variants
.ids-button {
  color: v-bind('buttonStyle.color');
  border: v-bind('buttonStyle.border');
  opacity: v-bind('buttonStyle.opacity');
  background: v-bind('buttonStyle.background');
  border-radius: v-bind('buttonStyle.borderRadius'); 
  &:hover {
    border: v-bind('buttonStyle.hoverBorder');
    background: v-bind('buttonStyle.hoverBackground');    
  }

  &:focus {
    outline-offset: 2px;
    border: v-bind('buttonStyle.focusedBorder');
    background: v-bind('buttonStyle.focusedBackground');
    opacity: var(--comp-buttons-size-spacious-border, 1);
    border-radius: var(--comp-buttons-size-spacious-border-radius, 1000px);
    outline:  var(--comp-buttons-focused-outline-size-outline, 3px) solid var(--base-color-dark, rgba(0, 0, 0, 1));
  }
  &:active {
    border: v-bind('buttonStyle.activeBorder');
    background: v-bind('buttonStyle.activeBackground');
    outline: none;
  }
  &:disabled {
    color: v-bind('buttonStyle.disabledColor');
    border: v-bind('buttonStyle.disabledBorder');
    background: v-bind('buttonStyle.disabledBackground');
  }
}

</style>
