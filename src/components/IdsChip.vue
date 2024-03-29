
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
  color: `var(--ids-comp-chips-${props.mode}-color-fg-${props.variant}-enabled)`,
  borderRadius: `var(--ids-comp-chips-size-${props.size}-border-radius, 6px)`,
  background: `var(--ids-comp-chips-${props.mode}-color-bg-${props.variant}-enabled)`,
  border: `var(--ids-comp-chips-size-${props.size}-border, 1px) solid var(--ids-comp-chips-${props.mode}-color-border-${props.variant}-enabled, rgba(255, 255, 255, 0.00))`,
  
  //hovered
  hoverBackground: `var(--ids-comp-chips-${props.mode}-color-bg-${props.variant}-hovered)`,
  hoverBorder: `var(--ids-comp-chips-size-${props.size}-border, 1px) solid var(--ids-comp-chips-${props.mode}-color-border-${props.variant}-hovered, rgba(255, 255, 255, 0.00))`,
  
  //focused
  focusedBackground: `var(--ids-comp-chips-${props.mode}-color-bg-${props.variant}-focused)`,
  focusedBorder: `var(--ids-comp-chips-size-${props.size}-border, 1px) solid var(--ids-comp-chips-${props.mode}-color-border-${props.variant}-focused, rgba(255, 255, 255, 0.00))`,
  focusBorderRadius: `var(--ids-comp-chips-size-${props.size}-border-radius, 6px)`,
  
  //active
  activeBackground: `var(--ids-comp-chips-${props.mode}-color-bg-${props.variant}-pressed)`,
  activeBorder: `var(--ids-comp-chips-size-${props.size}-border, 1px) solid var(--ids-comp-chips-${props.mode}-color-border-${props.variant}-pressed, rgba(255, 255, 255, 0.00))`,  

  //disabled
  disabledColor: `var(--ids-comp-chips-${props.mode}-color-fg-${props.variant}-disabled)`,
  disabledBackground: `var(--ids-comp-chips-${props.mode}-color-bg-${props.variant}-disabled)`,
  disabledBorder: `var(--ids-comp-chips-size-${props.size}-border, 1px) solid var(--ids-comp-chips-${props.mode}-color-border-${props.variant}-disabled, rgba(255, 255, 255, 0.00))`,

  //icon sizes
  iconWidth: `var(--ids-comp-chips-size-${props.size}-icon)`,
  iconHeight: `var(--ids-comp-chips-size-${props.size}-icon)`,
});
</script>

<template>
  <button :class="[size, 'ids-chip']" type="button">
    <component :is="props.leadingIcon" class="icon-size"></component>
    <slot></slot>
    <component :is="props.trailingIcon"  class="icon-size"></component>
  </button>
</template>

<style scoped lang="scss">
//icon sizes
.icon-size {
  gap: 16px;
  display: flex;
  align-items: flex-start;
  width: v-bind('chipStyle.iconWidth');
  height: v-bind('chipStyle.iconHeight');
}

//common
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
  gap: var(--ids-comp-chips-size-compact-gap, 4px);
  height: var(--ids-comp-chips-size-compact-height, 24px);
  padding: var(--ids-comp-chips-size-compact-padding-y, 8px) var(--ids-comp-chips-size-compact-padding-x, 8px);
}

.comfortable {
  @include common;
  font-size: 14px;
  line-height: 20px;
  letter-spacing: 0.1px;
  gap: var(--ids-comp-chips-size-comfortable-gap, 8px);
  height: var(--ids-comp-chips-size-comfortable-height, 32px);
  padding: var(--ids-comp-chips-size-comfortable-padding-y, 6px) var(--ids-comp-chips-size-comfortable-padding-x, 20px);
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
    outline:  var(--ids-comp-chips-focused-outline-size-outline, 3px) solid var(--base-color-dark, rgba(0, 0, 0, 1));
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
}

  .w-5 {
    width: 20px;
  }
  .h-5 {
    height: 20px;
  }
</style>
