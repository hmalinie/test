<template>
  <section>
    <slot></slot>
  </section>
</template>

<script>
export default {
  name: 'Step',
  props: {
    image: {
      type: String,
      required: true,
    },
  },
  created() {
    this.$parent.addStep({
      image: this.image,
    });
  },
};
</script>

<style lang="scss" scoped>
section {
  box-shadow: 0 3px 6px #ccc;
  padding: 32px 24px;
  background: #fff;
  border-top: 1px solid #eee;
}
</style>
