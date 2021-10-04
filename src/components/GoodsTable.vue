<template>
  <section class="goods-table">
    <h2 class="goods-table__title">Товары</h2>
    <transition-group name="list">
      <Product
        v-for="product in goods"
        :key="`goods-table__item--${product.id}`"
        @removeItem="$emit('removeItem', product)"
        :product="product"
      ></Product>
    </transition-group>
  </section>
</template>

<script>
import Product from "../components/Product.vue";

export default {
  name: "GoodsTable",
  props: {
    goods: {
      type: Array,
      required: true,
    },
  },
  components: {
    Product,
  },
};
</script>

<style scoped lang="scss">
.goods-table {
  display: grid;
  grid-gap: 16px;
  grid-template-columns: repeat(auto-fit, minmax(330px, 1fr));

  @media (max-width: 768px) {
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  }

  &__title {
    display: none;
  }
}

.list-enter-active, .list-leave-active {
  transition: all 0.5s;
}
.list-enter, .list-leave-to {
  opacity: 0;
  transform: scale(0.5);
}

.list-enter-to {
    animation: animationList 0.5s linear;
}

@keyframes animationList {
  0% {
    transform: scale(0.5);
  }

  100% {
    transform: scale(1);
  }
}
</style>