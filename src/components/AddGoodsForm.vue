<template>
  <div class="add-goods-form">
    <UiInput
      v-model.trim="product.title"
      inputType="text"
      placeholder="Введите наименование товара"
      :empty="errorTitle"
      :class="{ 'add-goods-form__item--error': error }"
      class="add-goods-form__item"
    >
      Наименование товара
    </UiInput>
    <UiInput
      v-model.trim="product.text"
      text
      :empty="errorText"
      placeholder="Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк"
      class="add-goods-form__item"
      >Описание товара
    </UiInput>
    <UiInput
      v-model.trim="product.src"
      :empty="errorSrc"
      inputType="text"
      placeholder="Введите ссылку"
      class="add-goods-form__item"
    >
      Ссылка на изображение товара
    </UiInput>
    <UiInput
      v-model.trim="product.price"
      :empty="errorPrice"
      inputType="text"
      placeholder="12 000"
      class="add-goods-form__item"
    >
      Цена товара
    </UiInput>
    <UiButton
      @click="createProduct"
      text="Добавить товар"
      class="add-goods-form__button"
    />
  </div>
</template>

<script>
import UiInput from "./uiComponents/UiInput/UiInput.vue";
import UiButton from "./uiComponents/UiButton/UiButton.vue";

export default {
  name: "AddGoogsForm",
  components: {
    UiInput,
    UiButton,
  },
  data() {
    return {
      isActive: false,
      product: {
        id: "",
        title: "",
        text: "",
        src: "",
        price: "",
      },
      errorTitle: false,
      errorText: false,
      errorSrc: false,
      errorPrice: false,
    };
  },
  methods: {
    createProduct() {
      this.product.id = Date();
      this.validationForm(this.product);

      if (this.isActive === true) {
        this.$emit("createNewProduct", this.product);
        this.product = {
          id: "",
          title: "",
          text: "",
          src: "",
          price: "",
        };
      }
    },
    validationForm(product) {
      product.title === ""
        ? (this.errorTitle = true)
        : (this.errorTitle = false);

      product.text === "" 
        ? (this.errorText = true) 
        : (this.errorText = false);

      product.src === "" 
        ? (this.errorSrc = true) 
        : (this.errorSrc = false);

      product.price === ""
        ? (this.errorPrice = true)
        : (this.errorPrice = false);

      if (
        this.errorTitle === true ||
        this.errorText === true ||
        this.errorSrc === true ||
        this.errorPrice === true
      ) {
        this.isActive = false;
      } else {
        this.isActive = true;
      }
    },
  },
};
</script>

<style scoped lang="scss">
.add-goods-form {
  background: hsl(45, 100%, 99%);
  box-shadow: 0px 20px 30px hsla(0, 0%, 0%, 0.04),
    0px 6px 10px hsla(0, 0%, 0%, 0.04);
  border-radius: 4px;
  padding: 24px;

  &__item {
    margin-bottom: 16px;
  }

  &__button {
    width: 100%;
  }
}
</style>