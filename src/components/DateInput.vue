<template>
  <div class="date-input">
    <v-menu
      :close-on-content-click="false"
      :nudge-right="40"
      lazy
      transition="scale-transition"
      offset-y
      full-width
      max-width="290px"
      min-width="290px"
      v-model="menuOpen"
    >
      <template v-slot:activator="{ on }">
        {{ toFrom }}
        <input
          v-model="dateFormatted"
          hint="DD/MM/YYYY format"
          persistent-hint
          :disabled="disabled"
          prepend-icon="event"
          @click="menuOpen = true"
          @blur="updateDate"
          v-on="on"
        />
      </template>

      <v-date-picker
        v-model="selectedDate"
        no-title
        @input="menuOpen = false"
      ></v-date-picker>
    </v-menu>
  </div>
</template>

<script>
export default {
  props: {
    value: Date, // Valor da data vinculado ao componente
    disabled: Boolean,
    toFrom: String,
  },
  data() {
    return {
      selectedDate: this.value,
      menuOpen: false,
    };
  },
  computed: {
    dateFormatted: {
      get() {
        return this.formatDate(this.selectedDate);
      },
      set(value) {
        this.selectedDate = this.parseDate(value);
      },
    },
  },

  methods: {
    formatDate(date) {
      if (!date) return null;

      const [year, month, day] = date.split("-");
      return `${day}/${month}/${year}`;
    },
    parseDate(date) {
      if (!date) return null;

      const [day, month, year] = date.split("/");
      return `${year}-${month.padStart(2, "0")}-${day.padStart(2, "0")}`;
    },
    updateDate() {
      // Dispara o evento 'input' com a data atualizada
      this.$emit("input", this.selectedDate);
    },
  },
};
</script>

<style scoped>
input {
  border: 2px solid black;
  width: 100px;
  height: 30px;
  border-radius: 6px;
  padding: 5px;
}
.date-input:not(.is-radios) {
  opacity: 0.3;
}
.date-input.is-radios {
  opacity: 1;
}
</style>
