
<script setup lang="ts">
import { reactive } from 'vue';

const props = withDefaults(defineProps<{
  mode?: "filled" | "outlined",
  size?: "compact" | "comfortable",
  variant?: "primary" | "secondary" | "brand" | "error" | "success" | "warning" | "light" | "dark",
  leadingIcon?: Object | undefined,
  trailingIcon?: Object | undefined,
}>(), {
  mode: 'filled',
  size: 'comfortable',
  variant: 'primary',
});

const chipStyle = reactive({
  //enabled
  //opacity: `var(--comp-chips-size-${props.size}-border, 1)`,
  color: `var(--comp-chips-${props.mode}-color-bg-fg-${props.variant}-enabled)`,
  borderRadius: `var(--comp-chips-size-${props.size}-border-radius, 6px)`,
  background: `var(--comp-chips-${props.mode}-color-bg-${props.variant}-enabled)`,
  border: `var(--comp-chips-size-${props.size}-border, 1px) solid var(--comp-chips-${props.mode}-color-border-${props.variant}-enabled, rgba(255, 255, 255, 0.00))`,
  
  //hovered
  hoverBackground: `var(--comp-chips-${props.mode}-color-bg-${props.variant}-hovered)`,
  hoverBorder: `var(--comp-chips-size-${props.size}-border, 1px) solid var(--comp-chips-${props.mode}-color-border-${props.variant}-hovered, rgba(255, 255, 255, 0.00))`,
  
  //focused
  focusedBackground: `var(--comp-chips-${props.mode}-color-bg-${props.variant}-focused)`,
  focusedBorder: `var(--comp-chips-size-${props.size}-border, 1px) solid var(--comp-chips-${props.mode}-color-border-${props.variant}-focused, rgba(255, 255, 255, 0.00))`,
  focusBorderRadius: `var(--comp-chips-size-${props.size}-border-radius, 6px)`,
  
  //disabled
  disabledColor: `var(--comp-chips-${props.mode}-color-fg-${props.variant}-disabled)`,
  disabledBackground: `var(--comp-chips-${props.mode}-color-bg-${props.variant}-disabled)`,
  disabledBorder: `var(--comp-chips-size-${props.size}-border, 1px) solid var(--comp-chips-${props.mode}-color-border-${props.variant}-disabled, rgba(255, 255, 255, 0.00))`,

  //active
  activeBackground: `var(--comp-chips-${props.mode}-color-bg-${props.variant}-pressed)`,
  activeBorder: `var(--comp-chips-size-${props.size}-border, 1px) solid var(--comp-chips-${props.mode}-color-border-${props.variant}-pressed, rgba(255, 255, 255, 0.00))`,  
});
</script>

<template>
  <button :class="[size, 'ids-chip']" type="button">
    <component :is="props.leadingIcon" class="w-5 h-5"></component>
    <slot></slot>
    <component :is="props.trailingIcon"  class="w-5 h-5"></component>
  </button>
</template>

<style scoped lang="scss">

@mixin common {
  flex-shrink: 0;  
  font-weight: 500;
  width: fit-content;
  align-items: center;
  display: inline-flex;
  justify-content: center;
}

//sizes
.compact {
  @include common;
  font-size: 12px;
  line-height: 16px; 
  letter-spacing: 0.5px;
  gap: var(--comp-chips-size-compact-gap, 4px);
  height: var(--comp-chips-size-compact-height, 24px);
  padding: var(--comp-chips-size-compact-padding-y, 8px) var(--comp-chips-size-compact-padding-x, 8px);
}

.comfortable {
  @include common;
  font-size: 14px;
  line-height: 20px;
  letter-spacing: 0.1px;
  gap: var(--comp-chips-size-comfortable-gap, 8px);
  height: var(--comp-chips-size-comfortable-height, 32px);
  padding: var(--comp-chips-size-comfortable-padding-y, 6px) var(--comp-chips-size-comfortable-padding-x, 20px);
}

//variants
.ids-chip {
  color: v-bind('chipStyle.color');
  border: v-bind('chipStyle.border');
  background: v-bind('chipStyle.background');
  border-radius: v-bind('chipStyle.borderRadius'); 
  &:hover {
    border: v-bind('chipStyle.hoverBorder');
    background: v-bind('chipStyle.hoverBackground');    
  }
  &:focus-within {
    outline-style: solid;
    outline-offset: 2px;
    border: v-bind('chipStyle.focusedBorder');
    background: v-bind('chipStyle.focusedBackground');
    border-radius: v-bind('chipStyle.focusBorderRadius');
    outline:  var(--comp-chips-focused-outline-size-outline, 3px) solid var(--base-color-dark, rgba(0, 0, 0, 1));
  }
  &:active {
    border: v-bind('chipStyle.activeBorder');
    background: v-bind('chipStyle.activeBackground');
    outline: none;
  }
  &:disabled {
    color: v-bind('chipStyle.disabledColor');
    border: v-bind('chipStyle.disabledBorder');
    background: v-bind('chipStyle.disabledBackground');
  }

  .w-5 {
    width: 20px;
  }
  .h-5 {
    height: 20px;
  }
}

</style>