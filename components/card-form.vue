<template>
  <div class="card-form-component flex column shrink-0 as-start p-24">
    <div class="input-item required">
      <div class="title flex c-violet">Наименование товара</div>
      <input
        v-model="name"
        type="text"
        placeholder="Введите наименование товара"
        class="c-dark"
      />
    </div>

    <div class="input-item">
      <div class="title flex c-violet">Описание товара</div>
      <textarea
        v-model="description"
        class="c-dark"
        placeholder="Введите описание товара"
      ></textarea>
    </div>

    <div class="input-item required">
      <div class="title flex c-violet">Ссылка на изображение товара</div>
      <input
        v-model="img"
        type="url"
        placeholder="Введите ссылку"
        class="c-dark"
      />
    </div>
    <div class="input-item required">
      <div class="title flex c-violet">Цена товара</div>
      <input
        v-model="price"
        type="number"
        placeholder="Введите цену"
        class="c-dark"
      />
    </div>
    <button
      :disabled="!enable"
      class="add-button fw-600 flex a-center j-center"
      @click="add"
    >
      Добавить товар
    </button>
  </div>
</template>

<script>
export default {
  name: 'CardFormPage',
  data() {
    return {
      name: null,
      description: null,
      img: null,
      price: null,
    }
  },
  computed: {
    enable() {
      return this.name && this.img && this.price
    },
  },
  methods: {
    add() {
      if (!this.enable) {
        return
      }
      this.$emit('add', {
        name: this.name,
        img: this.img,
        description: this.description,
        price: this.price,
      })
    },
  },
}
</script>

<style lang="scss" scoped>
.card-form-component {
  position: sticky;
  top: 24px;
  width: 332px;
  height: 440px;
  margin-right: 16px;
  border-radius: 4px;
  background-color: #fffefb;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  @include md {
    width: 100%;
    position: relative;
    top: 0;
    margin-bottom: 16px;
  }
  .input-item {
    margin-bottom: 16px;
    &:last-child {
      margin-bottom: 24px;
    }
    &.required {
      .title::after {
        content: '';
        align-self: start;
        width: 4px;
        height: 4px;
        background-color: #ff8484;
        border-radius: 100%;
      }
    }
    input {
      width: 100%;
      height: 36px;
      padding-left: 16px;
      border: none;
      border-radius: 4px;
      font-size: 12px;
      line-height: 15px;
      background-color: #fffefb;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
      &.error {
        border: 1px solid red;
      }
      &::placeholder {
        color: #b4b4b4;
      }
      &:focus {
        outline: none;
        box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
      }
    }
    textarea {
      width: 100%;
      height: 108px;
      padding-top: 10px;
      padding-left: 16px;
      font-size: 12px;
      line-height: 15px;
      background: #fffefb;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
      border: none;
      resize: none;
      border-radius: 4px;
      &::placeholder {
        color: #b4b4b4;
      }
      &:focus {
        outline: none;
        box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
      }
    }
  }
  .title {
    font-size: 10px;
    line-height: 13px;
    letter-spacing: -0.02em;
    margin-bottom: 4px;
  }
  .add-button {
    font-family: 'Inter', Arial, Helvetica, sans-serif;
    width: 100%;
    height: 36px;
    border-radius: 10px;
    font-size: 12px;
    line-height: 15px;
    letter-spacing: -0.02em;
    background-color: #7bae73;
    color: #fff;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    cursor: default;
    &[disabled] {
      color: #b4b4b4;
      background-color: #eee;
    }
    &:not([disabled]) {
      cursor: pointer;
      &:hover {
        box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
      }
      &:active {
        opacity: 0.8;
      }
    }
  }
}
</style>
