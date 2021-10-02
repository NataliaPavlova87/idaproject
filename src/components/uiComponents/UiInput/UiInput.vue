<template>
  <div class="input">
    <label class="input__label">
      <span class="input__title">
        <slot></slot>
      </span>
      <textarea
        v-if="text"
        :placeholder="placeholder"
        @input="inputUpdate"
        class="input__item input__item--text"
      ></textarea>
      <input
        v-else
        :type="inputType"
        :placeholder="placeholder"
        :value="modelValue"
        @input="inputUpdate"
        class="input__item"
      />
    </label>
    <span v-if="empty" class="input__error">Поле является обязательным</span>
  </div>
</template>

<script>
export default {
  name: "UiInput",
  props: {
    inputType: {
      type: String,
      default: "text",
    },
    placeholder: {
      type: String,
      default: "",
    },
    empty: {
      type: Boolean,
      default: false,
    },
    text: {
      type: Boolean,
      default: false,
    },
    modelValue: [Number, String],
  },
  methods: {
    inputUpdate(e) {
      this.$emit("update:modelValue", e.target.value);
    },
  },
};
</script>

<style scoped lang="scss">
.input {
  --input-color-error: hsl(0, 100%, 76%);
  display: flex;
  flex-direction: column;

  &__label {
    display: flex;
    flex-direction: column;
  }

  &__title {
    font-size: 10px;
    line-height: 13px;
    letter-spacing: -0.02em;
    color: hsl(243, 13%, 33%);
    position: relative;
    margin-bottom: 4px;
    align-self: flex-start;

    &::before {
      content: "";
      display: block;
      position: absolute;
      height: 4px;
      width: 4px;
      border-radius: 50%;
      background-color: var(--input-color-error);
      right: -5px;
      top: 0;
    }
  }

  &__error {
    font-size: 8px;
    line-height: 10px;
    letter-spacing: -0.02em;
    color: var(--input-color-error);
    margin-top: 4px;
  }

  &__item {
    background: hsl(45, 100%, 99%);
    box-shadow: 0px 2px 5px hsla(0, 0%, 0%, 0.1);
    border-radius: 4px;
    padding: 10px 16px;
    font-size: 12px;
    line-height: 15px;
    color: hsl(0, 0%, 25%);
    border: 1px solid transparent;
    transition: border-color 0.2s;

    &--text {
      min-height: 280px;
    }

    &--is-empty {
      border-color: var(--input-color-error);
    }

    &:focus {
      border-color: hsla(0, 0%, 0%, 0.1);
    }

    ::placeholder {
      font-size: 12px;
      line-height: 15px;
      color: hsl(0, 0%, 25%);
    }
  }
}
</style>