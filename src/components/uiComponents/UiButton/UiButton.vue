<template>
  <button :class="{'button--is-active': isActive}" class="button" title="text">
    <span class="button__text">
      {{ text }}
    </span>
  </button>
</template>

<script>
export default {
  name: "UiButton",
  props: {
    text: {
      type: String,
      default: "",
    },
    props: {
      isActive: {
        type: Boolean,
        default: false,
      },
    },
  },
};
</script>

<style scoped lang="scss">
.button {
  display: flex;
  align-items: center;
  justify-content: center;
  background: #eeeeee;
  border-radius: 10px;
  padding: 10px;
  border: 1px solid transparent;
  transition: opacity 0.2s, border-color 0.2s;
  font-family: "Inter", sans-serif;
  pointer-events: none;

  &--is-active {
    pointer-events: auto;
      background: red;
  }

  &:hover {
    opacity: 0.7;
  }

  &:focus {
    border: 1px solid hsl(0, 0%, 71%);
  }

  &__text {
    display: block;
    max-width: 100%;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
    font-weight: 600;
    font-size: 12px;
    text-align: center;
    letter-spacing: -0.02em;
    color: hsl(0, 0%, 71%);
  }
}
</style>