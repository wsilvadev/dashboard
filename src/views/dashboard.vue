<template>
  <div class="container">
    <div class="wip">Visao geral</div>
    <div class="container-card">
      <div class="false-group">
        <div
          v-for="(item, index) in falseItems"
          :key="index"
          :class="{ falseItem: item }"
        >
          <card-dashboard-vue
            :isSubscribers="item.isSubscribers"
            :title="item.title"
            :value="item.value"
          />
        </div>
      </div>
      <div class="true-group">
        <div
          v-for="(item, index) in trueItems"
          :key="index"
          :class="{ item: item }"
        >
          <card-dashboard-vue
            :isSubscribers="item.isSubscribers"
            :title="item.title"
            :value="item.value"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import CardDashboardVue from "@/components/CardDashboard.vue";

export default {
  name: "GridExample",
  components: {
    CardDashboardVue,
  },
  data() {
    return {
      api: [
        { isSubscribers: false, title: "Saldo total", value: 2344234 },
        { isSubscribers: false, title: "Faturado", value: 2344234 },
        { isSubscribers: false, title: "À faturar", value: 2344234 },
        { isSubscribers: true, title: "Total de Assinantes", value: 234429 },
        { isSubscribers: true, title: "Assinantes Torcedores", value: 234423 },
        { isSubscribers: true, title: "Assinantes Voucher", value: 234542 },
        { isSubscribers: true, title: "Assinantes Sócios", value: 23444 },
        { isSubscribers: true, title: "Assinantes Cortesia", value: 2348 },
      ],
      trueItems: [],
      falseItems: [],
    };
  },
  created() {
    this.api.forEach((item) => {
      if (item.isSubscribers) {
        this.trueItems.push(item);
      } else {
        this.falseItems.push(item);
      }
    });
  },
};
</script>

<style scoped>
.container {
  padding: 100px;
  height: 100%;
}
.wip {
  font-size: 40px;
  margin-bottom: 200px;
}

.container-card {
  width: 100%;
  display: flex;
  flex-direction: space-between;
  gap: 20px;
}

.true-group {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  gap: 20px;
}

.item {
  width: calc(50% - 10px); /* Dois itens por linha, com espaço entre eles */
  margin-bottom: 10px;
  padding: 0;
  margin: 0;
  /* Espaço inferior entre os itens */
}

/* Estilo específico para o quarto e quinto itens */
.item:nth-child(3),
.item:nth-child(4),
.item:nth-child(5) {
  width: calc(33.33% - 14px);
}
.false-group {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  gap: 20px;
}
.falseItem {
  width: calc(100% - 0px); /* Dois itens por linha, com espaço entre eles */
  margin-bottom: 10px;
  padding: 0;
  margin: 0;
}
.falseItem:nth-child(2),
.falseItem:nth-child(3) {
  width: calc(50% - 10px);
}
</style>
