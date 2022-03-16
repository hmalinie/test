<template>
  <div class="form-item">
    <div class="label-wrapper">
      <label>{{ label }}</label>
    </div>

    <div class="image-radio-button-group">
      <ImageRadioButton
        v-for="(item, index) in list"
        :key="index"
        :name="item.name"
        :image="item.image"
        :value="item.value"
        :text="item.text"
        :checked="item.value === value"
        @input="$emit('input', $event)"
      />
    </div>
  </div>
</template>

<script>
import ImageRadioButton from './ImageRadioButton';

export default {
  name: 'RadioGroupItem',
  components: { ImageRadioButton },
  props: {
    label: {
      type: String,
      required: true,
    },
    list: {
      type: Array,
      required: true,
      validator: list => list.every(item => item.name && item.image && item.text),
    },
    value: {
      type: String,
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

.image-radio-button-group {
  > * {
    margin-right: 32px;

    &:last-child {
      margin-right: 0;
    }
  }
}
</style>
