<script setup lang="ts">
import { reactive } from "vue";

const props = withDefaults(
  defineProps<{
    type?: "vertical" | "horizontal";
    size?: "compact" | "comfortable" | "spacious";
    variant?:
      | "surface"
      | "primary"
      | "secondary"
      | "brand"
      | "error"
      | "success"
      | "warning"
      | "light"
      | "dark";
    width?: string;
    height?: string;
  }>(),
  {
    type: "horizontal",
    size: "comfortable",
    variant: "primary",
  },
);

const DividerStyle = reactive({
  //enabled
  background: ` var(--ids-comp-divider-color-fg-${props.variant}-enabled)`,
  borderRadius: `var(--ids-comp-divider-size-${props.size}-border-radius, 0px)`,
  width: props.width,
  height: props.height,
});
</script>

<template>
  <div :class="[type, size, 'ids-divider']"></div>
</template>

<style scoped lang="scss">
@mixin common {
  display: flex;
  align-items: center;
  justify-content: center;
}

//sizes
.vertical {
  &.compact {
    @include common;
    align-self: stretch;
    width: var(--ids-comp-divider-size-compact-width, 1px);
  }
  &.comfortable {
    @include common;
    align-self: stretch;
    width: var(--ids-comp-divider-size-comfortable-width, 2px);
  }
  &.spacious {
    @include common;
    align-self: stretch;
    width: var(--ids-comp-divider-size-spacious-width, 4px);
  }
}

.horizontal {
  &.compact {
    @include common;
    align-self: stretch;
    height: var(--ids-comp-divider-size-compact-height, 1px);
  }
  &.comfortable {
    @include common;
    align-self: stretch;
    height: var(--ids-comp-divider-size-comfortable-height, 2px);
  }
  &.spacious {
    @include common;
    align-self: stretch;
    height: var(--ids-comp-divider-size-spacious-height, 4px);
  }
}
//variants
.ids-divider {
  width: v-bind("DividerStyle.width");
  height: v-bind("DividerStyle.height");
  background: v-bind("DividerStyle.background");
  border-radius: v-bind("DividerStyle.borderRadius");
}
</style>
