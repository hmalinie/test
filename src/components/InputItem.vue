<template>
  <div class="form-item">
    <div class="label-wrapper">
      <label :for="id">{{ label }}</label>
      <span>{{ description }}</span>
    </div>

    <div>
      <input
        :id="id"
        :type="type"
        :placeholder="placeholder"
        :value="value"
        required
        @input="$emit('input', $event.target.value)"
      />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    id: {
      type: String,
      required: true,
    },
    type: {
      type: String,
      default: 'text',
      validator: type => ['text', 'email'].includes(type),
    },
    placeholder: {
      type: String,
      required: true,
    },
    label: {
      type: String,
      required: true,
    },
    description: {
      type: String,
      default: '',
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
}
</style>
