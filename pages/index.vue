<template>
  <section class="w-container">
    <div class="header flex a-center j-between">
      <div class="title fw-600 c-dark">Добавление товара</div>
      <button class="sort-button flex a-center j-center">
        По умолчанию
        <v-icon name="arrow-down" />
      </button>
    </div>
    <div class="wrapper flex">
      <Form @add="add" />
      <div class="flex flex-1 wrap g-16" tabindex="0">
        <Card
          v-for="(product, index) in products"
          :key="index"
          :fill="product"
          @remove="remove"
        />
      </div>
    </div>
  </section>
</template>

<script>
import Form from '@/components/card-form'
import Card from '@/components/card'
import vIcon from '@/components/icons/icon'

export default {
  name: 'IndexPage',
  components: {
    Form,
    vIcon,
    Card,
  },
  data() {
    return {
      products: [],
    }
  },
  created() {
    this.add({
      id: Date.now(),
      name: 'Наименование товара',
      img: 'polaroid.png',
      description:
        'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
      price: 10000,
    })
  },
  methods: {
    add(product) {
      this.products.push({ ...product, id: Date.now() })
    },
    remove(id) {
      this.products = this.products.filter((p) => p.id !== id)
    },
  },
}
</script>

<style lang="scss" scoped>
.w-container {
  max-width: 1440px;
  margin: 0 auto;
  padding: 0 32px;
  padding-top: 32px;
  @include md {
    padding: 0 15px;
    padding-top: 15px;
  }
  .title {
    font-size: 28px;
    line-height: 35px;
    @include md {
      font-size: 20px;
    }
  }
  .sort-button {
    width: 120px;
    height: 36px;
    font-size: 12px;
    line-height: 15px;
    color: #b4b4b4;
    background-color: #fffefb;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    svg {
      margin-left: 5px;
    }
    &:hover {
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
    }
    &:active {
      opacity: 0.8;
    }
  }
  .wrapper {
    margin-top: 16px;
    @include md {
      flex-direction: column;
    }
  }
}
</style>
