<template>
  <article class="product">
    <div class="product__top">
      <button @click="$emit('removeItem', product)" class="product__button product-button">
        <svg
          class="product-button__icon"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 16 16"
        >
          <path
            d="M10.2 5.8c-.2 0-.4.2-.4.4v7a.4.4 0 0 0 .8 0v-7c0-.2-.2-.4-.4-.4ZM5.8 5.8c-.2 0-.4.2-.4.4v7a.4.4 0 0 0 .8 0v-7c0-.2-.2-.4-.4-.4Z"
          />
          <path
            d="M2.6 4.8V14c0 .5.2 1 .5 1.4.4.4.8.6 1.4.6h7c.5 0 1-.2 1.4-.6.3-.3.5-.9.5-1.4V4.8a1.4 1.4 0 0 0-.3-2.9h-2v-.4A1.5 1.5 0 0 0 9.7 0H6.3a1.5 1.5 0 0 0-1.5 1.5v.4H3a1.4 1.4 0 0 0-.3 2.9Zm9 10.5H4.4c-.7 0-1.2-.6-1.2-1.3V4.8h9.4V14c0 .7-.5 1.3-1.2 1.3Zm-6-13.8a.7.7 0 0 1 .7-.8h3.4a.7.7 0 0 1 .7.8v.4H5.6v-.4ZM2.9 2.7h10.2A.7.7 0 1 1 13 4H2.9a.7.7 0 1 1 0-1.3Z"
          />
          <path
            d="M8 5.8c-.2 0-.4.2-.4.4v7a.4.4 0 0 0 .8 0v-7c0-.2-.2-.4-.4-.4Z"
          />
        </svg>
      </button>
      <img class="product__image" :src="product.src" :alt="product.title" />
    </div>
    <div class="product__content">
      <h3 class="product__title">{{ product.title }}</h3>
      <p class="product__text">{{ product.text }}</p>
      <span class="product__price">{{ product.price }} руб.</span>
    </div>
  </article>
</template>

<script>
export default {
  name: "Product",
  props: {
    product: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped lang="scss">
.product {
  $self: &;
  --product-text-color: hsl(0, 0%, 25%);
  display: flex;
  flex-direction: column;
  background: hsl(45, 100%, 99%);
  box-shadow: 0px 20px 30px hsla(0, 0%, 0%, 0.04),
    0px 6px 10px hsla(0, 0%, 0%, 0.02);
  border-radius: 4px;

  &:hover {
    #{$self} {
      &__button {
        pointer-events: auto;
        opacity: 1;
      }
    }
  }

  &__top {
    height: 200px;
    position: relative;
    border-top-left-radius: inherit;
    border-top-right-radius: inherit;
  }

  &__image {
    display: block;
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: center center;
    border-top-left-radius: inherit;
    border-top-right-radius: inherit;
  }

  &__button {
    position: absolute;
    top: -10px;
    right: -10px;
    width: 32px;
    height: 32px;
    opacity: 0;
    pointer-events: none;
  }

  &__content {
    display: flex;
    flex-direction: column;
    padding: 16px;
    flex-grow: 1;
  }

  &__price {
    margin-top: auto;
    font-weight: 600;
    font-size: 24px;
    line-height: 30px;
    color: var(--product-text-color);
  }

  &__title {
    font-weight: 600;
    font-size: 20px;
    line-height: 25px;

    color: var(--product-text-color);
    padding-bottom: 16px;
  }

  &__text {
    font-size: 16px;
    line-height: 20px;

    color: var(--product-text-color);
    padding-bottom: 30px;
  }
}

.product-button {
  background: hsl(0, 100%, 76%);
  box-shadow: 0px 2px 4px hsla(0, 0%, 0%, 0.1);
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: opacity 0.5s transform 0.5s;

  &:focus,
  &:hover {
    transform: scale(1.1);
  }

  &__icon {
    display: block;
    width: 16px;
    height: 16px;
    fill: hsl(0, 0%, 100%);
  }
}
</style>