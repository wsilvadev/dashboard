<template>
  <v-card class="mx-auto" width="400" height="300">
    <v-card-title
      >RELATÓRIO <br />
      {{ formatTitle }}
    </v-card-title>
    <v-radio-group v-model="radios" column style="margin-left: 20px;">
      <v-radio value="completo">
        <template v-slot:label>
          <div class="container-full">
            <strong
              :class="{
                isRadiosFull: radios == 'completo',
              }"
              >COMPLETO</strong
            >
          </div>
        </template>
      </v-radio>
      <v-radio value="date">
        <template v-slot:label>
          <div class="container-date">
            <date-input
              :class="{
                'is-radios': radios == 'date',
              }"
              :to-from="'DE'"
              :value="startDateFormatted"
              :disabled="radios != 'date'"
              @blur="startDate = parseDate(startDateFormatted)"
            />
            <date-input
              :class="{
                'is-radios': radios == 'date',
              }"
              :to-from="'ATÉ'"
              :value="endDateFormatted"
              :disabled="radios != 'date'"
              @blur="endDate = parseDate(endDateFormatted)"
            />
          </div>
        </template>
      </v-radio>
    </v-radio-group>
    <div class="container-btn">
      <v-btn class="button">
        <img src="../assets/download-icon.svg" />
        Download
      </v-btn>
    </div>
  </v-card>
</template>
<script>
import DateInput from "@/components/DateInput.vue";

export default {
  components: {
    DateInput,
  },
  data() {
    return {
      radios: "completo",
      startDate: null,
      endDate: null,
      startDateFormatted: null,
      endDateFormatted: null,
    };
  },
  props: {
    title: String,
  },

  computed: {
    formatTitle() {
      const title = this.title.split(" ");
      const lastWord = title[title.length - 1].toUpperCase();
      if (
        lastWord === "TORCEDORES" ||
        lastWord === "CORTESIA" ||
        lastWord === "VOUNCHER" ||
        lastWord === "ASSINANTES" ||
        lastWord === "SÓCIOS"
      ) {
        return `TOTAL DE ${lastWord}`;
      } else {
        return this.title.toUpperCase();
      }
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
  },
};
</script>
<style scoped>
.container-full.isRadiosFull {
  opacity: 1;
}

.container-full :not(.isRadiosFull) {
  opacity: 0.3;
}
.theme--light.v-btn.v-btn--has-bg {
  background-color: #fff;
}
.v-btn {
  border: 1px solid black;
  border-radius: 15px;
  color: #000000;
}
.container-btn {
  margin-left: 20px;
  margin-top: 10px;
}
.container-btn img {
  margin-right: 10px;
  width: 20px;
}
.container-date {
  align-items: center;
  display: flex;
  flex-direction: row;
  font-weight: 700;
  gap: 5px;
  justify-content: space-between;
  z-index: 99999;
}
</style>
<style>
.v-menu__content {
  border: 2px solid black;
  border-radius: 20px;
}
.v-overlay__scrim {
  background-color: transparent !important;
}
.v-card > .v-card__title {
  font-size: 30px;
}
</style>
