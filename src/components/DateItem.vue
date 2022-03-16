<template>
  <div class="form-item">
    <div class="label-wrapper">
      <label :for="id">{{ label }}</label>
    </div>

    <div class="inputs">
      <select v-model="day" :id="id" required>
        <option :value="null">Jour</option>
        <option v-for="i in days" :key="i" :value="i">{{ i }}</option>
      </select>
      <select v-model="month" required>
        <option :value="null">Mois</option>
        <option v-for="i in months" :key="i" :value="i">{{ i }}</option>
      </select>
      <select v-model="year" required>
        <option :value="null">Année</option>
        <option v-for="i in years" :key="i" :value="i">{{ i }}</option>
      </select>
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
    label: {
      type: String,
      required: true,
    },
    value: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      day: null,
      month: null,
      year: null,
    };
  },
  watch: {
    year() {
      this.onChange();
    },
    month() {
      this.onChange();
    },
    day() {
      this.onChange();
    },
  },
  computed: {
    years() {
      const years = [];
      for (let i = 0; i < 100; i++) {
        years.push(String(2022 - i));
      }
      return years;
    },
    months() {
      const months = [];
      for (let i = 1; i <= 12; i++) {
        months.push(i < 10 ? `0${String(i)}` : String(i));
      }
      return months;
    },
    days() {
      const days = [];
      for (let i = 1; i <= 31; i++) {
        days.push(i < 10 ? `0${String(i)}` : String(i));
      }
      return days;
    },
  },
  methods: {
    onChange() {
      if (this.year && this.month && this.day) {
        this.$emit('input', `${this.year}-${this.month}-${this.day}`);
      } else {
        this.$emit('input', '');
      }
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

.inputs {
  display: flex;

  select {
    margin-right: 10px;

    &:last-child {
      margin-right: 0;
    }
  }
}
</style>
