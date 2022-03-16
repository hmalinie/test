<template>
  <div class="container">
    <button
      type="button"
      v-for="(i, index) in Array(5).fill(null)"
      :class="{ selected: index < displayed }"
      :data-index="index"
      :key="index"
      @click="$emit('input', index + 1)"
    ></button>
  </div>
</template>

<script>
export default {
  name: 'Stars',
  props: {
    value: {
      type: Number,
      required: true,
    },
  },
  mounted() {
    this.$el.addEventListener('mousemove', this.onMouseMove);
    this.$el.addEventListener('mouseleave', this.onMouseLeave);
  },
  beforeDestroy() {
    this.$el.removeEventListener('mousemove', this.onMouseMove);
    this.$el.removeEventListener('mouseleave', this.onMouseLeave);
  },
  data() {
    return {
      displayed: 0,
    };
  },
  watch: {
    value() {
      this.displayed = this.value;
    },
  },
  methods: {
    onMouseMove(e) {
      if (this.value === 0 && e.target.nodeName === 'BUTTON') {
        this.displayed = Number(e.target.dataset.index) + 1;
      }
    },
    onMouseLeave() {
      if (this.value === 0) {
        this.displayed = 0;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  display: inline-block;
}

button {
  background: transparent;
  border: none;
  font-size: 24px;
  cursor: pointer;

  &:before {
    content: '☆';
  }

  &.selected:before {
    content: '★';
  }
}
</style>
