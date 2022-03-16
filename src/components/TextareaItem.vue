<template>
  <div class="form-item">
    <div class="label-wrapper">
      <label :for="id">{{ label }}</label>
    </div>
    <div>
      <textarea
        :id="id"
        :value="value"
        @input="$emit('input', $event.target.value)"
        required
        :placeholder="`Décrivez votre expérience avec votre nouveau produit Tediber ?
Qu'est-ce qui vous plait le plus ?
Pourquoi le recommanderiez-vous ?`">
      </textarea>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TextareaItem',
  props: {
    id: {
      type: String,
      required: true,
    },
    label: {
      type: String,
      required: true,
    },
    placeholder: {
      type: String,
      required: true,
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
