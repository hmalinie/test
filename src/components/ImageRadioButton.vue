<template>
  <label :for="id">
    <input
      :id="id"
      type="radio"
      :name="name"
      :value="value"
      hidden
      @input="onChange"
    />

    <div class="container">
      <img :src="`/images/${this.image}.svg`"/>
      <p class="label">{{ text }}</p>
    </div>
  </label>
</template>

<script>
let cpt = 0;

export default {
  name: 'ImageRadioButton',
  props: {
    image: {
      type: String,
      required: true,
    },
    text: {
      type: String,
      required: true,
    },
    value: {
      type: String,
      required: true,
    },
    name: {
      type: String,
      required: true,
    },
  },
  computed: {
    id() {
      return `image-radio-button-${++cpt}`;
    },
  },
  methods: {
    onChange(e) {
      if (e.target.checked) {
        this.$emit('input', e.target.value);
      }
    },
  },
};
</script>

<style lang="scss" scoped>
label {
  cursor: pointer;
  display: inline-block;
}

.container {
  img {
    height: 90px;
    border: 1px solid #ccc;
    display: block;
    margin: 0 auto 8px;
  }

  p {
    text-align: center;
    text-transform: none;
    letter-spacing: normal;
    font-weight: normal;
  }
}

input:checked ~ .container {
  img {
    border: 1px solid orange;
    box-shadow: inset 0 0 0 1px orange;
  }

  p {
    color: orange;
  }
}
</style>
