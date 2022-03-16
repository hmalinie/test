<template>
  <form :class="`visible-${currentStep}`">
    <div class="navigation">
      <button
        type="button"
        class="item"
        v-for="(step, index) in steps"
        :key="index"
        :class="{ selected: currentStep === index, before: index < currentStep }"
        @click="onItemClick(index)"
      >
        <img :src="`/images/${step.image}`"/>
        <div class="blank"></div>
      </button>
    </div>

    <div class="content">
      <slot></slot>
    </div>
  </form>
</template>

<script>
export default {
  name: 'Steps',
  props: {
    currentStep: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      steps: [],
    };
  },
  watch: {
    currentStep() {
      window.scrollTo({ top: 0, behavior: 'smooth' });
    },
  },
  methods: {
    addStep(step) {
      this.steps.push(step);
    },
    onItemClick(index) {
      if (index < this.currentStep) {
        this.$emit('update:currentStep', index);
      }
    },
  },
};
</script>

<style lang="scss" scoped>
form {
  display: flex;
}

.navigation {
  display: none;

  @media (min-width: 768px) {
    display: block;
  }

  .item {
    padding: 16px 32px;
    opacity: 0.4;
    background: transparent;
    border: none;
    display: block;

    .blank {
      display: none;
    }

    &.selected {
      background-color: #fff;
      box-shadow: -2px 3px 6px #ccc;
      position: relative;
      opacity: 1;
      border-top: 1px solid #eee;

      .blank {
        display: block;
        position: absolute;
        right: 0;
        top: 0;
        bottom: 0;
        width: 10px;
        background: #fff;
        margin-right: -10px;
      }
    }

    &.before {
      cursor: pointer;
    }

    img {
      display: block;
      margin: auto;
      width: 80px;
      max-height: 50px;
    }
  }
}

.content {
  width: 100%;
}

.content > * {
  display: none;
}

.visible-0 .content > *:nth-child(1) {
  display: block;
}

.visible-1 .content > *:nth-child(2) {
  display: block;
}

.visible-2 .content > *:nth-child(3) {
  display: block;
}
</style>
