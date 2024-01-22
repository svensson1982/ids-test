
<script setup lang="ts">
import { reactive } from 'vue';

const props = withDefaults(defineProps<{
  type?: "submit" | "button" | "reset",
  mode?: "filled" | "outlined" | "standard",
  size?: "compact" | "comfortable" | "spacious",
  variant?: "primary" | "secondary" | "brand" | "error" | "success" | "warning" | "light" | "dark" | "surface",
  icon?: Object | undefined,
}>(), {
  type: 'button',
  mode: 'filled',
  size: 'comfortable',
  variant: 'primary',
});

const iconButtonStyle = reactive({
  //enabled
  borderRadius: `var(--comp-icon-button-size-${props.size}-border-radius, 1000px)`,
  background: ` var(--comp-icon-button-${props.mode}-color-bg-${props.variant}-enabled)`,
  border: `var(--comp-icon-button-size-${props.size}-border, 1px) solid var(--comp-icon-button-${props.mode}-color-border-${props.variant}-enabled, rgba(255, 255, 255, 0.00))`,

  //hovered
  hoverBackground: `var(--comp-icon-button-${props.mode}-color-bg-${props.variant}-hovered)`,
  hoverBorder: `var(--comp-icon-button-size-${props.size}-border, 1px) solid var(--comp-icon-button-${props.mode}-color-border-${props.variant}-hovered, rgba(255, 255, 255, 0.00))`,
  
  //focused
  focusedBackground: `var(--comp-icon-button-${props.mode}-color-bg-${props.variant}-focused)`,
  focusedBorder: `var(--comp-icon-button-size-${props.size}-border, 1px) solid var(--comp-icon-button-${props.mode}-color-border-${props.variant}-focused, rgba(255, 255, 255, 0.00))`,
  
  //active
  activeBackground: `var(--comp-icon-button-${props.mode}-color-bg-${props.variant}-pressed)`,
  activeBorder: `var(--comp-icon-button-size-${props.size}-border, 1px) solid var(--comp-icon-button-${props.mode}-color-border-${props.variant}-pressed, rgba(255, 255, 255, 0.00))`,  

  //disabled
  disabledColor: `var(--comp-icon-button-${props.mode}-color-fg-${props.variant}-disabled)`,
  disabledBackground: `var(--comp-icon-button-${props.mode}-color-bg-${props.variant}-disabled)`,
  disabledBorder: `var(--comp-icon-button-size-${props.size}-border, 1px) solid var(--comp-icon-button-${props.mode}-color-border-${props.variant}-disabled, rgba(255, 255, 255, 0.00))`, 

  iconWidthHeight: `var(--comp-buttons-size-${props.size}-icon, 16px)`,
});

</script>

<template>
  <button :type="type" :class="[size, mode, variant, 'ids-icon-button']">
    <component :is="props.icon"></component>
  </button>
</template>

<style scoped lang="scss">

@mixin common {
  display: flex;
  flex-shrink: 0;
  align-items: center;
  justify-content: center;
}

//icons
// width: var(--comp-buttons-size-compact-icon, 16px);
// height: var(--comp-buttons-size-compact-icon, 16px);

// gap: 10px;

//sizes
.compact {
  @include common;
  gap: var(--comp-icon-button-size-compact-gap, 4px);
  font-size: var(--comp-buttons-size-compact-icon, 16px);
  width: var(--comp-icon-button-size-compact-width, 24px);
  height: var(--comp-icon-button-size-compact-height, 24px);
  padding: 0px;// var(--comp-icon-button-size-compact-padding-y, 6px) var(--comp-icon-button-size-compact-padding-x, 8px);
  & > svg { 
  //font-size: var(--comp-buttons-size-spacious-icon, 32px);
  padding: 5px;
  } 
}

.comfortable {
  @include common;
  gap: var(--comp-icon-button-size-comfortable-gap, 8px);
  font-size: var(--comp-buttons-size-comfortable-icon, 24px);
  width: var(--comp-icon-button-size-comfortable-width, 40px);
  height: var(--comp-icon-button-size-comfortable-height, 40px);
  padding: 0px; // var(--comp-icon-button-size-comfortable-padding-y, 10px) var(--comp-icon-button-size-comfortable-padding-x, 20px);
  & > svg { 
  //font-size: var(--comp-buttons-size-spacious-icon, 32px);
  padding: 5px;
  } 
}

.spacious {
  @include common;
  gap: var(--comp-icon-button-size-spacious-gap, 8px);
  //font-size: var(--comp-buttons-size-spacious-icon, 32px);
  width: var(--comp-icon-button-size-spacious-width, 56px);
  height: var(--comp-icon-button-size-spacious-height, 56px);
  padding: 0px ;//var(--comp-icon-button-size-spacious-padding-y, 16px) var(--comp-icon-button-size-spacious-padding-x, 24px);
  & > svg { 
  //font-size: var(--comp-buttons-size-spacious-icon, 32px);
  padding: 5px;
  } 
 
}

.filled {
  color: var(--comp-icon-button-filled-color-fg-primary-enabled);
  &:disabled {
    color: var(--comp-icon-button-filled-color-fg-disabled);
  }
}

//#app > section > div > button.comfortable.filled.primary.ids-icon-button > svg

.outlined {
  color: var(--comp-icon-button-filled-color-fg-primary-enabled);
  border: var(--comp-icon-button-size-comfortable-border, 1px) solid var(--comp-icon-button-outlined-color-border-success-enabled, #22C55E);
  &:disabled {
    color: var(--comp-icon-button-filled-color-fg-disabled);
  }
}

//variants
.ids-icon-button {
  //color: v-bind('iconButtonStyle.color');
  border: v-bind('iconButtonStyle.border');
  background: v-bind('iconButtonStyle.background');
  border-radius: v-bind('iconButtonStyle.borderRadius'); 
  &:hover {
    border: v-bind('iconButtonStyle.hoverBorder');
    background: v-bind('iconButtonStyle.hoverBackground');    
  }
  &:focus {
    outline-offset: 2px;
    border: v-bind('iconButtonStyle.focusedBorder');
    background: v-bind('iconButtonStyle.focusedBackground');
    opacity: var(--comp-icon-button-size-spacious-border, 1);
    border-radius: var(--comp-icon-button-size-spacious-border-radius, 1000px);
    outline:  var(--comp-icon-button-focused-outline-size-outline, 3px) solid var(--base-color-dark, rgba(0, 0, 0, 1));
  }
  &:active {
    border: v-bind('iconButtonStyle.activeBorder');
    background: v-bind('iconButtonStyle.activeBackground');
    outline: none;
  }
  &:disabled {
    color: v-bind('iconButtonStyle.disabledColor');
    border: v-bind('iconButtonStyle.disabledBorder');
    background: v-bind('iconButtonStyle.disabledBackground');
  }

}

</style>
