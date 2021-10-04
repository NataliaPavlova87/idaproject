<template>
  <div class="add-goods-page">
    <header class="add-goods-page__header add-goods-page-header">
      <h2 @click="sortDate" class="add-goods-page-header__title">
        Добавление товара
      </h2>
      <UiSelect
        @select="optionSelect"
        :options="selectOptions"
        :selected="selected"
        class="add-goods-page-header__select"
      />
    </header>
    <AddGoodsForm
      @createNewProduct="createProduct"
      class="add-goods-page__form"
    />
    <GoodsTable
      @removeItem="removeProduct"
      :goods="goods"
      class="add-goods-page__table"
    />
  </div>
</template>

<script>
import UiSelect from "../components/uiComponents/uiSelect/UiSelect.vue";
import AddGoodsForm from "../components/AddGoodsForm.vue";
import GoodsTable from "../components/GoodsTable.vue";

export default {
  name: "AddGoogsPage",
  components: {
    UiSelect,
    AddGoodsForm,
    GoodsTable,
  },
  data() {
    return {
      selected: "По умолчанию",
      sortedProducts: [],
      selectOptions: [
        {
          name: "min",
          value: "По убыванию",
        },
        {
          name: "max",
          value: "По возрастанию",
        },
      ],
      sortedGoodsItem: [],
      goods: [
        {
          id: 1,
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк.Довольно-таки интересное описание товара в несколько строк",
          price: 12000,
          src: "https://d.radikal.ru/d02/2110/f5/935f7210758f.jpg",
        },
        {
          id: 2,
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: 13000,
          src: "https://d.radikal.ru/d02/2110/f5/935f7210758f.jpg",
        },
        {
          id: 3,
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: 10500,
          src: "https://d.radikal.ru/d02/2110/f5/935f7210758f.jpg",
        },
        {
          id: 4,
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: 60000,
          src: "https://d.radikal.ru/d02/2110/f5/935f7210758f.jpg",
        },
        {
          id: 5,
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: 10000,
          src: "https://d.radikal.ru/d02/2110/f5/935f7210758f.jpg",
        },
      ],
    };
  },
  methods: {
    createProduct(product) {
      return this.goods.push(product);
    },
    removeProduct(product) {
      this.goods = this.goods.filter((p) => p.id !== product.id);
    },
    optionSelect(option) {
      this.selected = option.value;
      this.sortedGoods(option);
    },
    sortedGoods(option) {
      for (let i = 0; this.goods.length > i; i++) {
        this.goods.price = +this.goods[i].price;
      }

      if (option.name === "min") {
        this.goods.sort((a, b) => b.price - a.price);
      }

      if (option.name === "max") {
        this.goods.sort((a, b) => a.price - b.price);
      }
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

input:focus {
  outline: none;
}

textarea {
  resize: none;
}

textarea:focus {
  outline: none;
}

button {
  border: none;
  cursor: pointer;
}

button:focus {
  outline: none;
}
</style>

<style scoped lang="scss">
.add-goods-page {
  background-color: hsla(45, 100%, 99%, 0.8);
  padding: 32px;
  font-family: "Source Sans Pro", sans-serif;
  min-height: 100vh;
  display: grid;
  grid-gap: 16px;
  grid-template-areas: "header header" "form table";
  grid-template-columns: 330px 1fr;
  align-items: flex-start;

  @media (max-width: 768px) {
    grid-template-areas: "header" "form" "table";
    grid-template-columns: 100%;
    padding-left: 10px;
    padding-right: 10px;
  }

  &__header {
    padding-bottom: 16px;
    grid-area: header;
  }

  &__form {
    grid-area: form;
  }

  &__table {
    grid-area: table;
  }
}

.add-goods-page-header {
  display: flex;
  justify-content: space-between;
  align-items: center;

  @media (max-width: 768px) {
    flex-direction: column;
  }

  &__title {
    font-weight: 600;
    font-size: 28px;
    line-height: 35px;
    color: hsl(0, 0%, 25%);
  }

  &__select {
    min-width: 135px;
  }
}
</style>
