<script setup lang="ts">
import { reactive } from "vue";

const props = withDefaults(
  defineProps<{
    mode?: "text" | "filled";
    size?: "compact" | "comfortable" | "spacious";
    variant?: "surface";
    leadingIcon?: Object | undefined;
    trailingIcon?: Object | undefined;
    isDisabled?: boolean;
  }>(),
  {
    mode: "filled",
    isDisabled: false,
    size: "comfortable",
    variant: "surface",
  },
);

const actionItemButtonStyle = reactive({
  //enabled
  opacity: `var(--ids-comp-action-item-button-size-${props.size}-border, 1)`,
  color: `var(--ids-comp-action-item-button-${props.mode}-color-fg-surface-enabled)`,
  borderRadius: `var(--ids-comp-action-item-button-size-${props.size}-border-radius, 1000px)`,
  background: ` var(--ids-comp-action-item-button-${props.mode}-color-bg-${props.variant}-enabled)`,
  border: `var(--ids-comp-action-item-button-size-${props.size}-border, 1px) solid var(--ids-comp-action-item-button-${props.mode}-color-border-${props.variant}-enabled, rgba(255, 255, 255, 0.00))`,

  //hovered
  hoverBackground: `var(--ids-comp-action-item-button-${props.mode}-color-bg-${props.variant}-hovered)`,
  hoverBorder: `var(--ids-comp-action-item-button-size-${props.size}-border, 1px) solid var(--ids-comp-action-item-button-${props.mode}-color-border-${props.variant}-hovered, rgba(255, 255, 255, 0.00))`,

  //focused
  focusedBackground: `var(--ids-comp-action-item-button-${props.mode}-color-bg-${props.variant}-focused)`,
  focusedBorder: `var(--ids-comp-action-item-button-size-${props.size}-border, 1px) solid var(--ids-comp-action-item-button-${props.mode}-color-border-${props.variant}-focused, rgba(255, 255, 255, 0.00))`,

  //active
  activeBackground: `var(--ids-comp-action-item-button-${props.mode}-color-bg-${props.variant}-pressed)`,
  activeBorder: `var(--ids-comp-action-item-button-size-${props.size}-border, 1px) solid var(--ids-comp-action-item-button-${props.mode}-color-border-${props.variant}-pressed, rgba(255, 255, 255, 0.00))`,

  //disabled
  disabledColor: `var(--ids-comp-action-item-button-${props.mode}-color-fg-${props.variant}-disabled)`,
  disabledBackground: `var(--ids-comp-action-item-button-${props.mode}-color-bg-${props.variant}-disabled)`,
  disabledBorder: `var(--ids-comp-action-item-button-size-${props.size}-border, 1px) solid var(--ids-comp-action-item-button-${props.mode}-color-border-${props.variant}-disabled, rgba(255, 255, 255, 0.00))`,

  //icon sizes
  iconWidthHeight: `var(--ids-comp-action-item-button-size-${props.size}-icon)`,
});
</script>

<template>
  <button
    type="button"
    :class="[size, 'ids-button']"
    :disabled="isDisabled"
    :aria-disabled="isDisabled ? 'true' : undefined"
  >
    <component
      :is="props.leadingIcon"
      class="icon-size"
      aria-hidden="true"
    ></component>
    <slot></slot>
    <component
      :is="props.trailingIcon"
      class="icon-size"
      aria-hidden="true"
    ></component>
  </button>
</template>

<style scoped lang="scss">
//icon sizes
.icon-size {
  gap: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  width: v-bind("actionItemButtonStyle.iconWidthHeight");
  height: v-bind("actionItemButtonStyle.iconWidthHeight");
}

@mixin common {
  flex-shrink: 0;
  font-weight: 700;
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
  gap: var(--ids-comp-action-item-button-size-compact-gap, 4px);
  height: var(--ids-comp-action-item-button-size-compact-height, 24px);
  padding: var(--ids-comp-action-item-button-size-compact-padding-y, 6px)
    var(--ids-comp-action-item-button-size-compact-padding-x, 8px);
}

.comfortable {
  @include common;
  font-size: 14px;
  line-height: 20px;
  gap: var(--ids-comp-action-item-button-size-comfortable-gap, 8px);
  height: var(--ids-comp-action-item-button-size-comfortable-height, 40px);
  padding: var(--ids-comp-action-item-button-size-comfortable-padding-y, 10px)
    var(--ids-comp-action-item-button-size-comfortable-padding-x, 20px);
}

.spacious {
  @include common;
  font-size: 18px;
  line-height: 24px;
  gap: var(--ids-comp-action-item-button-size-spacious-gap, 8px);
  height: var(--ids-comp-action-item-button-size-spacious-height, 56px);
  padding: var(--ids-comp-action-item-button-size-spacious-padding-y, 16px)
    var(--ids-comp-action-item-button-size-spacious-padding-x, 24px);
}

//variants
.ids-button {
  color: v-bind("actionItemButtonStyle.color");
  border: v-bind("actionItemButtonStyle.border");
  opacity: v-bind("actionItemButtonStyle.opacity");
  background: v-bind("actionItemButtonStyle.background");
  border-radius: v-bind("actionItemButtonStyle.borderRadius");

  &:hover {
    border: v-bind("actionItemButtonStyle.hoverBorder");
    background: v-bind("actionItemButtonStyle.hoverBackground");
  }

  &:focus {
    outline-offset: 2px;
    border: v-bind("actionItemButtonStyle.focusedBorder");
    background: v-bind("actionItemButtonStyle.focusedBackground");
    opacity: var(--ids-comp-action-item-button-size-spacious-border, 1);
    border-radius: var(
      --ids-comp-action-item-button-size-spacious-border-radius,
      1000px
    );
    outline: var(
        --ids-comp-action-item-button-focused-outline-size-outline,
        3px
      )
      solid var(--base-color-dark, rgba(0, 0, 0, 1));
  }

  &:active {
    border: v-bind("actionItemButtonStyle.activeBorder");
    background: v-bind("actionItemButtonStyle.activeBackground");
    outline: none;
  }

  &:disabled {
    color: v-bind("actionItemButtonStyle.disabledColor");
    border: v-bind("actionItemButtonStyle.disabledBorder");
    background: v-bind("actionItemButtonStyle.disabledBackground");
  }
}
</style>
