<template>
  <div class="form-item">
    <div class="label-wrapper">
      <label>{{ label }}</label>
    </div>

    <Stars :value="value" @input="$emit('input', $event)"/>
  </div>
</template>

<script>
import Stars from './Stars';

export default {
  name: 'StarsItem',
  components: { Stars },
  props: {
    label: {
      type: String,
      required: true,
    },
    value: {
      type: Number,
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped>
.form-item {
  margin-bottom: 24px;

  &:last-child {
    margin-bottom: 0;
  }

  .label-wrapper {
    display: block;
    margin-bottom: 16px;

    label {
      text-transform: uppercase;
      letter-spacing: 3px;
      font-weight: bold;
    }
  }

  input[type="text"], input[type="email"], select {
    height: 40px;
    padding: 0 8px;
    width: 100%;
    border: 1px solid #ccc;
    font-size: 16px;

    ::placeholder {
      color: #ccc;
      font-size: 16px;
    }
  }

  textarea {
    font-family: Lato, sans-serif;
    width: 100%;
    border: 1px solid #ccc;
    padding: 8px;
    font-size: 16px;
    height: 120px;
  }
}
</style>
