<template>
  <v-card
    class="card"
    :class="{ customCard: isSubscribers == true }"
    elevation="2"
  >
    <div class="card-header">
      <span class="currency-symbol">
        <img src="../assets/people.svg" v-if="isSubscribers == true" />
        <span v-else> R$</span>
      </span>
      <div class="title-wrapper">
        <span class="card-title">{{ title }}</span>
        <img src="../assets/download-icon.svg" />
      </div>
    </div>
    <div class="value-wrapper">
      <span class="card-value">{{ formatValue }}</span>
    </div>
  </v-card>
</template>

<script>
export default {
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
};
</script>

<style scoped>
.card {
  min-width: 100%; /* Ajuste o tamanho do card conforme necessário */
  text-align: center;
  height: 200px;
  background: #000000;
  border-radius: 20px;
  border-top-left-radius: 90px;
}
.card.customCard {
  background: transparent;
  border-top-left-radius: 94px;
  border: 1px solid black;
}

.card-value {
  font-size: 3vw;
  font-weight: bold;
  color: #ffffff;
}
.card.customCard .card-value {
  color: #000000;
  font-size: 90px;
}
.v-card > *:last-child:not(.v-btn):not(.v-chip):not(.v-avatar) {
  border-bottom-left-radius: 0;
  border-bottom-right-radius: 0;
}
.currency-symbol {
  position: absolute;
  font-size: 30px;
  width: 60px;
  background-color: #ffffff;
  height: 60px;
  top: 0;
  left: 0;
  border-radius: 20px;
  z-index: 10;
  padding-top: 10px;
}
.card.customCard .currency-symbol {
  border-bottom: 1px solid black;
  border-right: 1px solid black;
}
.currency-symbol::before {
  content: "";
  position: absolute;
  background-color: transparent;
  bottom: -50px;
  left: 0;
  height: 50px;
  width: 25px;
  border-top-left-radius: 20px;
  box-shadow: 0 -40px 0 0 #ffffff;
  z-index: -1;
}
.card.customCard .currency-symbol::before {
  left: -1px;
  border-top: 1px solid black;
}
.currency-symbol::after {
  content: "";
  position: absolute;
  background-color: transparent;
  right: -37px;
  top: -12px;
  height: 50px;
  transform: rotate(-90deg);
  width: 25px;
  border-top-right-radius: 20px;
  box-shadow: 0 -40px 0 0 #ffffff;
  z-index: -1;
}
.card.customCard .currency-symbol::after {
  top: -13px;
  border-top: 1px solid black;
}
.title-wrapper {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  height: 70px;
  padding-left: 70px;
}
.card.customCard .title-wrapper {
  padding: 0;
  justify-content: center;
}
.title-wrapper img {
  width: 40px;
  margin-right: 30px;
}
.card.customCard .title-wrapper img {
  position: absolute;
  right: 0;
}
.value-wrapper {
  display: flex;
  padding: 20px;
  padding-right: 50px;
  justify-content: end;
}
.card.customCard .value-wrapper {
  padding: 20px;
  justify-content: center;
  height: 60%;
  font-size: 106px;
  line-height: 100px;
}
.card-title {
  font-weight: bold;
  font-size: 20px;
  color: #fff; /* Tamanho do título */
}
.card.customCard .card-title {
  color: #000000;
}
.currency-symbol img {
  width: 40px;
}
</style>
