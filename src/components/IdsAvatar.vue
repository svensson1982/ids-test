<script setup lang="ts">
import { reactive } from "vue";

const props = withDefaults(
  defineProps<{
    size?: "compact" | "comfortable" | "spacious";
    variant?: "surface" | "primary" | "secondary" | "light" | "dark";
    image?: string;
  }>(),
  {
    size: "comfortable",
    variant: "primary",
  },
);

const avatarStyle = reactive({
  //enabled
  color: `var(--ids-comp-avatar-color-fg-${props.variant}-enabled)`,
  borderRadius: `var(--ids-comp-avatar-size-spacious-border-radius, 62.5rem)`,
  background: ` var(--ids-comp-avatar-color-bg-${props.variant}-enabled)`,
  border: `var(--ids-comp-avatar-size-${props.size}-border, 1px) solid var(--ids-comp-avatar-color-border-${props.variant}-enabled, rgba(255, 255, 255, 0.00))`,

  //hovered
  hoverBackground: `var(--ids-comp-avatar-color-bg-${props.variant}-hovered)`,
  hoverBorder: `var(--ids-comp-avatar-size--border, 1px) solid var(--ids-comp-avatar-color-border-${props.variant}-hovered, rgba(255, 255, 255, 0.00))`,

  //focused
  focusedBackground: `var(--ids-comp-avatar-color-bg-${props.variant}-focused)`,
  focusedBorder: `var(--ids-comp-avatar-size-border, 1px) solid var(--ids-comp-avatar-color-border-${props.variant}-focused, rgba(255, 255, 255, 0.00))`,

  //active
  activeBackground: `var(--ids-comp-avatar-color-bg-${props.variant}-pressed)`,
  activeBorder: `var(--ids-comp-avatar-size-${props.size}-border, 1px) solid var(--ids-comp-avatar-color-border-${props.variant}-pressed, rgba(255, 255, 255, 0.00))`,

  //image sizes
  width: `var(--ids-comp-avatar-size-${props.size}-width)`,
  height: `var(--ids-comp-avatar-size-${props.size}-height)`,
  iconPadding: `var(--ids-comp-avatar-size-${props.size}-padding-y) var(--ids-comp-avatar-size-${props.size}-padding-x)`,
  iconColor: `var(--ids-comp-avatar-color-fg-${props.variant}-enabled)`,

});
</script>

<template>
  <button type="button" :class="[size, 'ids-button']">
    <slot v-if="$slots.default"></slot>
    <div v-else>
      <img v-if="image" :src="image" class="img-size" />
      <svg v-else width="52" height="52" viewBox="0 0 52 52" fill="none" xmlns="http://www.w3.org/2000/svg"
        class="icon-size">
        <mask id="mask0_3222_9853" style="mask-type:alpha" maskUnits="userSpaceOnUse" x="7" y="5" width="38" height="47">
          <path fill-rule="evenodd" clip-rule="evenodd"
            d="M7.79999 44.3943C12.0726 39.0451 18.6378 35.6199 26 35.6199C33.3622 35.6199 39.9274 39.0451 44.2 44.3943C39.554 49.0914 33.1154 52 26 52C18.8846 52 12.446 49.0914 7.79999 44.3943ZM37.6569 16.9C37.6569 23.3617 32.4379 28.6 26 28.6C19.562 28.6 14.343 23.3617 14.343 16.9C14.343 10.4382 19.562 5.19995 26 5.19995C32.4379 5.19995 37.6569 10.4382 37.6569 16.9Z"
            :fill="avatarStyle.iconColor" />
        </mask>
        <g mask="url(#mask0_3222_9853)">
          <rect width="52" height="52" fill="currentColor" />
        </g>
      </svg>
      <!-- <img  src="@/assets/icons/user-avatar.svg" class="icon-size" alt="User Icon" /> -->
    </div>
  </button>
</template>

<style scoped lang="scss">
@mixin common {
  padding: 5px;
  display: flex;
  font-style: normal;
  text-align: center;
  align-items: center;
  flex-direction: column;
  justify-content: center;
}

//icon size
.icon-size {
  gap: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  width: 100%; // v-bind('avatarStyle.width');
  height: 100%; //v-bind('avatarStyle.height');
}

//icon padding
.icon-padding {
  padding: v-bind("avatarStyle.iconPadding");
}

//image size
.img-size {
  border-radius: 50%;
  align-items: center;
  flex-direction: column;
  vertical-align: middle;
  justify-content: center;
  width: v-bind("avatarStyle.width");
  height: v-bind("avatarStyle.height");
}

//sizes
.compact {
  @include common;
  font-weight: 500;
  line-height: 1rem;
  font-size: 0.6875rem;
  letter-spacing: 0.03125rem;
  width: var(--ids-comp-avatar-size-compact-height, 1.5rem);
  height: var(--ids-comp-avatar-size-compact-width, 1.5rem);
}

.comfortable {
  @include common;
  font-weight: 400;
  font-size: 0.875rem;
  line-height: 1.25rem;
  letter-spacing: 0.01563rem;
  width: var(--ids-comp-avatar-size-comfortable-width, 2.5rem);
  height: var(--ids-comp-avatar-size-comfortable-height, 2.5rem);
}

.spacious {
  @include common;
  font-weight: 400;
  font-style: normal;
  font-size: 1.375rem;
  line-height: 1.75rem;
  width: var(--ids-comp-avatar-size-spacious-width, 4rem);
  height: var(--ids-comp-avatar-size-spacious-height, 4rem);
}

//variants
.ids-button {
  color: v-bind("avatarStyle.color");
  border: v-bind("avatarStyle.border");
  background: v-bind("avatarStyle.background");
  border-radius: v-bind("avatarStyle.borderRadius");

  &:hover {
    border: v-bind("avatarStyle.hoverBorder");
    background: v-bind("avatarStyle.hoverBackground");
  }

  &:focus {
    outline-offset: 2px;
    border: v-bind("avatarStyle.focusedBorder");
    background: v-bind("avatarStyle.focusedBackground");
    opacity: var(--ids-comp-buttons-size-spacious-border, 1);
    border-radius: var(--ids-comp-buttons-size-spacious-border-radius, 1000px);
    outline: var(--ids-comp-buttons-focused-outline-size-outline, 3px) solid var(--base-color-dark, rgba(0, 0, 0, 1));
  }

  &:active {
    border: v-bind("avatarStyle.activeBorder");
    background: v-bind("avatarStyle.activeBackground");
    outline: none;
  }
}
</style>
