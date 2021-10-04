<template>
  <div class="select">
    <div class="select__option">
      <button @click="isVisible" class="select__button">
        <span class="select__text"> {{ selected }}</span>
        <svg
          :class="{ 'select__icon--is-open': isOpen }"
          class="select__icon"
          viewBox="0 0 8 8"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M7.48532 3.24264L4.24268 6.48528L1.00003 3.24264"
            stroke="hsl(0, 0%, 71%)"
          />
        </svg>
      </button>
    </div>
    <div v-if="isOpen" class="select__content">
      <ul class="select__list">
        <li
          v-for="option in options"
          :key="option.name"
          class="select__option"
          @click="selectOption(option)"
        >
          <button class="select__button">
            <span class="select__text"> {{ option.value }} </span>
          </button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "UiSelect",
  data() {
    return {
      isOpen: false,
    };
  },
  props: {
    options: {
      type: Array,
      default: () => [],
    },
    selected: {
      type: String,
      default: "",
    },
  },
  methods: {
    isVisible() {
      this.isOpen = !this.isOpen;
    },
    selectOption(option) {
      this.$emit("select", option);
    },
    hideSelect() {
      this.isOpen = false;
    },
  },
};
</script>

<style scoped lang="scss">
.select {
  $self: &;
  background: hsl(45, 100%, 99%);
  box-shadow: 0px 2px 5px hsla(0, 0%, 0%, 0.1);
  border-radius: 4px;
  border: none;

  &:hover,
  &:focus {
    outline: none;
  }

  &__content {
    position: relative;
  }

  &__list {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    z-index: 1;
    transform: translateY(-2px);
    background: hsl(45, 100%, 99%);
    box-shadow: 0px 2px 5px hsla(0, 0%, 0%, 0.1);
    border-bottom-right-radius: 4px;
    border-bottom-left-radius: 4px;
    transition: height 0.5s;
    width: 100%;
  }

  &__option {
    width: 100%;
    list-style: none;
    display: block;
  }

  &__button {
    width: 100%;
    padding: 5px 16px;
    transition: background-color 0.2s;
    background-color: transparent;
    position: relative;
    text-align: left;

    &:hover,
    &:focus {
      background-color: #eeeeee;
    }
  }

  &__text {
    font-size: 12px;
    line-height: 15px;
    color: hsl(0, 0%, 71%);
  }

  &__icon {
    display: block;
    width: 8px;
    height: 8px;
    position: absolute;
    right: 16px;
    top: 8px;
    transition: transform 0.2s;

    &--is-open {
      transform: rotate(180deg);
    }
  }
}
</style>