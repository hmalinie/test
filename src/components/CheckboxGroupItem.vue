<template>
  <div class="form-item">
    <div class="label-wrapper">
      <label class="label">{{ label }}</label>
    </div>

    <div class="checkbox-list">
      <label
        :for="`checkbox-${id}-item-${index}`"
        v-for="(item, index) in list"
        :key="index"
      >
        <input
          :id="`checkbox-${id}-item-${index}`"
          type="checkbox"
          :value="item.value"
          :checked="value.includes(item.value)"
          @input="onChange($event)"
        />
        {{ item.label }}
      </label>
    </div>
  </div>
</template>

<script>
let cpt = 0;

export default {
  name: 'CheckboxGroupItem',
  props: {
    label: {
      type: String,
      required: true,
    },
    list: {
      type: Array,
      required: true,
    },
    value: {
      type: Array,
      required: true,
      validator: array => array.every(item => typeof item === 'string'),
    },
  },
  computed: {
    id() {
      return ++cpt;
    },
  },
  methods: {
    onChange(e) {
      const value = this.value.slice();
      if (e.target.checked) {
        value.push(e.target.value);
      } else {
        value.splice(value.indexOf(e.target.value), 1);
      }
      this.$emit('input', value);
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

.checkbox-list {
  label {
    display: block;
  }
}
</style>
