
<script setup lang="ts">
import { reactive } from 'vue';

const props = withDefaults(defineProps<{
  type?: "submit" | "button" | "reset" | undefined,
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
  //--comp-icon-button-standard-color-bg-primary-disabled
  //background: var(--comp-icon-button-standard-color-bg-primary-disabled
  color: `var(--ids-comp-icon-button-${props.mode}-color-fg-${props.variant}-enabled)`,
  borderRadius: `var(--ids-comp-icon-button-size-${props.size}-border-radius, 1000px)`,
  background: ` var(--ids-comp-icon-button-${props.mode}-color-bg-${props.variant}-enabled)`,
  border: `var(--ids-comp-icon-button-size-${props.size}-border, 1px) solid var(--ids-comp-icon-button-${props.mode}-color-border-${props.variant}-enabled, rgba(255, 255, 255, 0.00))`,

  //hovered
  hoverBackground: `var(--ids-comp-icon-button-${props.mode}-color-bg-${props.variant}-hovered)`,
  hoverBorder: `var(--ids-comp-icon-button-size-${props.size}-border, 1px) solid var(--ids-comp-icon-button-${props.mode}-color-border-${props.variant}-hovered, rgba(255, 255, 255, 0.00))`,

  //focused
  focusedBackground: `var(--ids-comp-icon-button-${props.mode}-color-bg-${props.variant}-focused)`,
  focusedBorder: `var(--ids-comp-icon-button-size-${props.size}-border, 1px) solid var(--ids-comp-icon-button-${props.mode}-color-border-${props.variant}-focused, rgba(255, 255, 255, 0.00))`,

  //active
  activeBackground: `var(--ids-comp-icon-button-${props.mode}-color-bg-${props.variant}-pressed)`,
  activeBorder: `var(--ids-comp-icon-button-size-${props.size}-border, 1px) solid var(--ids-comp-icon-button-${props.mode}-color-border-${props.variant}-pressed, rgba(255, 255, 255, 0.00))`,

  //disabled
  disabledColor: `var(--ids-comp-icon-button-${props.mode}-color-fg-${props.variant}-disabled)`,
  disabledBackground: `var(--ids-comp-icon-button-${props.mode}-color-bg-${props.variant}-disabled)`,
  disabledBorder: `var(--ids-comp-icon-button-size-${props.size}-border, 1px) solid var(--ids-comp-icon-button-${props.mode}-color-border-${props.variant}-disabled, rgba(255, 255, 255, 0.00))`,

  iconWidthHeight: `var(--ids-comp-icon-button-size-${props.size}-icon)`,
});

</script>

<template>
  <button :type="type" :class="[size, mode + '-mode']">
    <component :is="props.icon" class="icon-size"></component>
  </button>
</template>

<style scoped lang="scss"> @mixin common {
   display: flex;
   flex-shrink: 0;
   align-items: center;
   justify-content: center;
 }

 .icon-size {
   width: v-bind('iconButtonStyle.iconWidthHeight');
   height: v-bind('iconButtonStyle.iconWidthHeight');
 }

 //sizes
 .compact {
   @include common;
   gap: var(--ids-comp-icon-button-size-compact-gap, 4px);
   width: var(--ids-comp-icon-button-size-compact-width, 24px);
   height: var(--ids-comp-icon-button-size-compact-height, 24px);
   padding: 0px;
 }

 .comfortable {
   @include common;
   gap: var(--ids-comp-icon-button-size-comfortable-gap, 8px);
   width: var(--ids-comp-icon-button-size-comfortable-width, 40px);
   height: var(--ids-comp-icon-button-size-comfortable-height, 40px);
   padding: 0px;
 }

 .spacious {
   @include common;
   gap: var(--ids-comp-icon-button-size-spacious-gap, 8px);
   width: var(--ids-comp-icon-button-size-spacious-width, 56px);
   height: var(--ids-comp-icon-button-size-spacious-height, 56px);
   padding: 0px;
 }

 //variants
 .filled-mode,
 .outlined-mode {
   color: v-bind('iconButtonStyle.color');
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
     opacity: var(--ids-comp-icon-button-size-spacious-border, 1);
     border-radius: var(--ids-comp-icon-button-size-spacious-border-radius, 1000px);
     outline: var(--ids-comp-icon-button-focused-outline-size-outline, 3px) solid var(--base-color-dark, rgba(0, 0, 0, 1));
   }

   &:active {
     outline: none;
     border: v-bind('iconButtonStyle.activeBorder');
     background: v-bind('iconButtonStyle.activeBackground');
   }

   &:disabled {
     color: v-bind('iconButtonStyle.disabledColor');
     border: v-bind('iconButtonStyle.disabledBorder');
     background: v-bind('iconButtonStyle.disabledBackground');
   }
 }

 .standard-mode {
   border: none;
   color: v-bind('iconButtonStyle.color');
   background: v-bind('iconButtonStyle.background');
   border-radius: v-bind('iconButtonStyle.borderRadius');

   &:hover {
     background: v-bind('iconButtonStyle.hoverBackground');
     border: none;
   }

   &:focus {
     border: none;
     outline-offset: 2px;
     background: v-bind('iconButtonStyle.focusedBackground');
     opacity: var(--ids-comp-icon-button-size-spacious-border, 1);
     border-radius: var(--ids-comp-icon-button-size-spacious-border-radius, 1000px);
     outline: var(--ids-comp-icon-button-focused-outline-size-outline, 3px) solid var(--base-color-dark, rgba(0, 0, 0, 1));
   }

   &:active {
     border: none;
     outline: none;
     background: v-bind('iconButtonStyle.activeBackground');
   }

   &:disabled {
     border: none;
     color: v-bind('iconButtonStyle.disabledColor');
     background: v-bind('iconButtonStyle.disabledBackground');
   }
 }
</style>
