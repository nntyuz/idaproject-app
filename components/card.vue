<template>
  <div class="card-component flex column">
    <div class="card-img shrink-0">
      <img :src="fill.img" alt="Picture" />
    </div>
    <div class="flex column flex-1 p-16 pb-24">
      <div class="title fw-600 c-dark">{{ fill.name }}</div>
      <div v-show="fill.description" class="description c-dark">
        {{ fill.description }}
      </div>
      <div class="price fw-600 c-dark">{{ formatPrice(fill.price) }} руб.</div>
    </div>
    <button
      class="remove-button flex a-center j-center"
      @click="$emit('remove', fill.id)"
    >
      <v-icon name="bin" />
    </button>
  </div>
</template>
<script>
import vIcon from '@/components/icons/icon'

export default {
  name: 'CardComponent',
  components: {
    vIcon,
  },
  props: {
    fill: {
      type: Object,
      required: true,
    },
  },
  methods: {
    formatPrice(value) {
      const val = (value / 1).toFixed(0).replace(' ')
      return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ' ')
    },
  },
}
</script>
<style lang="scss" scoped>
.card-component {
  width: 332px;
  height: 423px;
  position: relative;
  border-radius: 4px;
  background-color: #fffefb;
  transition: 300ms ease;
  box-shadow: 0 20px 30px rgba(0, 0, 0, 0.04), 0 6px 10px rgba(0, 0, 0, 0.02);
  &:hover {
    box-shadow: 0 20px 30px rgba(0, 0, 0, 0.1), 0 6px 10px rgba(0, 0, 0, 0.05);
    .remove-button {
      opacity: 1;
    }
  }
  @include md {
    width: 100%;
  }
  .card-img {
    overflow: hidden;
    width: 100%;
    height: 200px;
    border-top-right-radius: 4px;
    border-top-left-radius: 4px;
    img {
      display: block;
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
  }
  .title {
    font-size: 20px;
    line-height: 25px;
    margin-bottom: 16px;
  }
  .description {
    margin-bottom: 32px;
    font-size: 16px;
    line-height: 20px;
  }
  .price {
    margin-top: auto;
    font-size: 24px;
    line-height: 30px;
  }
  .remove-button {
    opacity: 0;
    position: absolute;
    top: -8px;
    right: -8px;
    width: 32px;
    height: 32px;
    background: #ff8484;
    transition: 300ms ease;
    border-radius: 10px;
    svg {
      transition: 300ms ease;
      fill: #fff;
    }
    &:hover {
      background: #fff;
      svg {
        fill: #ff8484;
      }
    }
  }
}
</style>
