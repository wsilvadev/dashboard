<template>
  <div>
    <v-card
      class="card"
      :class="{
        customCard: isSubscribers == true,
      }"
      elevation="2"
    >
      <div class="card-header">
        <span class="currency-symbol">
          <img src="../assets/people.svg" v-if="isSubscribers == true" />
          <span v-else> R$</span>
        </span>
        <div class="title-wrapper">
          <span class="card-title">{{ title }}</span>

          <v-menu
            transition="scale-transition"
            v-model="menu"
            :close-on-content-click="false"
            location="end"
          >
            <template
              v-slot:activator="{
                props,
              }"
            >
              <v-btn icon class="icon" v-bind="props" @click="openMenu">
                <img src="../assets/download-icon.svg" />
              </v-btn>
            </template>
            <modal-download :title="title" />
          </v-menu>
        </div>
        <div class="value-wrapper">
          <span class="card-value">{{ formatValue }}</span>
        </div>
      </div>
    </v-card>
  </div>
</template>

<script>
import ModalDownload from "./ModalDownload.vue";
export default {
  data() {
    return {
      menu: false,
    };
  },
  components: {
    ModalDownload,
  },
  props: {
    title: String, // Título
    value: Number, // Valor
    isSubscribers: Boolean, //
  },
  computed: {
    formatValue() {
      let formattedValue;
      if (this.isSubscribers == true)
        formattedValue = this.value.toLocaleString("pt-BR");
      else
        formattedValue = this.value.toLocaleString("pt-BR", {
          style: "currency",
          currency: "BRL",
          minimumFractionDigits: 2, // Número mínimo de casas decimais
        });
      return formattedValue.replace("R$", "").trim();
    },
  },
  methods: {
    openMenu() {
      this.menu = true;
    },
  },
};
</script>

<style scoped>
.card {
  background: #000000;
  border-radius: 20px;
  border-top-left-radius: 90px;
  height: 200px;
  text-align: center;
  width: 100%;

  /* Ajuste o tamanho do card conforme necessário */
}

.card.customCard {
  background: transparent;
  border: 1px solid black;
  border-top-left-radius: 94px;
}

.card-value {
  color: #ffffff;
  font-size: 60px;
  font-weight: bold;
}
.card.customCard .card-value {
  color: #000000;
  font-size: 60px;
}
.v-card > *:last-child:not(.v-btn):not(.v-chip):not(.v-avatar) {
  border-bottom-left-radius: 0;
  border-bottom-right-radius: 0;
}
.currency-symbol {
  background-color: #c7c7c7;
  border-radius: 20px;
  font-size: 30px;
  height: 60px;
  left: 0;
  padding-top: 10px;
  position: absolute;
  top: 0;
  width: 60px;
  z-index: 1;
}
.card.customCard .currency-symbol {
  border-bottom: 1px solid black;
  border-right: 1px solid black;
}
.currency-symbol::before {
  background-color: transparent;
  border-top-left-radius: 20px;
  bottom: -50px;
  box-shadow: 0 -40px 0 0 #c7c7c7;
  content: "";
  height: 50px;
  left: 0;
  position: absolute;
  width: 25px;
  z-index: -1;
}
.card.customCard .currency-symbol::before {
  border-top: 1px solid black;
  left: -1px;
}
.currency-symbol::after {
  background-color: transparent;
  border-top-right-radius: 20px;
  box-shadow: 0 -40px 0 0 #c7c7c7;
  content: "";
  height: 50px;
  position: absolute;
  right: -37px;
  top: -12px;
  transform: rotate(-90deg);
  width: 25px;
  z-index: -1;
}
.card.customCard .currency-symbol::after {
  border-top: 1px solid black;
  top: -13px;
}
.title-wrapper {
  align-items: center;
  display: flex;
  flex-direction: row;
  height: 70px;
  justify-content: space-between;
  padding-left: 70px;
  width: 100%;
}
.card.customCard .title-wrapper {
  justify-content: center;
  padding: 0;
  width: 100%;
}
.title-wrapper .icon {
  margin-right: 30px;
  width: 40px;
}
.card.customCard .title-wrapper .icon {
  position: absolute;
  right: 0;
}
.value-wrapper {
  align-items: end;
  display: flex;
  height: 130px;
  justify-content: end;
  padding: 20px;
  padding-right: 50px;
}
.card.customCard .value-wrapper {
  align-items: end;
  justify-content: center;
}
.card-title {
  color: #fff;
  font-size: 20px;
  font-weight: bold;
  padding-top: 20px;
}
.card.customCard .card-title {
  color: #000000;
  width: 50%;
}
.currency-symbol img {
  width: 40px;
}
.icon img {
  width: 40px;
}
@media (max-width: 760px) {
  .card {
    height: 150px;
  }
  .value-wrapper {
    height: 80px;
  }

  .currency-symbol img {
    width: 20px;
  }
  .icon img {
    width: 20px;
  }
  .card-title {
    font-size: 10px;
    padding: 10px;
  }
  .title-wrapper .icon {
    margin-right: 5px;
  }
}
</style>
