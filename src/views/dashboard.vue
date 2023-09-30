<template>
  <div class="container">
    <div class="wip">Visao geral</div>
    <div class="container-card">
      <div class="false-group">
        <div
          v-for="(item, index) in falseItems"
          :key="index"
          :class="{
            falseItem: item,
          }"
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
          :class="{
            item: item,
          }"
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
        {
          isSubscribers: false,
          title: "Saldo total",
          value: 2344234,
        },
        {
          isSubscribers: false,
          title: "Faturado",
          value: 2344234,
        },
        {
          isSubscribers: false,
          title: "À faturar",
          value: 2344234,
        },
        {
          isSubscribers: true,
          title: "Total de Assinantes",
          value: 234429,
        },
        {
          isSubscribers: true,
          title: "Assinantes Torcedores",
          value: 234423,
        },
        {
          isSubscribers: true,
          title: "Assinantes Vouncher",
          value: 234542,
        },
        {
          isSubscribers: true,
          title: "Assinantes Sócios",
          value: 23444,
        },
        {
          isSubscribers: true,
          title: "Assinantes Cortesia",
          value: 2348,
        },
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
  height: 100%;
  padding: 100px;
}
.wip {
  font-size: 40px;
  margin-bottom: 200px;
}

.container-card {
  display: flex;
  gap: 20px;
  width: 100%;
}
.true-group {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  width: 100%;
}
.false-group {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  width: 100%;
}

.item {
  margin: 0;
  margin-bottom: 10px;
  padding: 0;
  width: calc(50% - 10px);
  /* Dois itens por linha, com espaço entre eles */
  /* Espaço inferior entre os itens */
}

/* Estilo específico para o quarto e quinto itens */
.item:nth-child(3),
.item:nth-child(4),
.item:nth-child(5) {
  width: calc(33.33% - 14px);
}
.item:nth-child(1)::v-deep .card-value {
  font-size: 6.6vmin;
  font-weight: 777;
}
.item:nth-child(2)::v-deep .card-value {
  font-size: 5vmin;
}
.item:nth-child(3)::v-deep .card-value {
  font-size: 4.6vmin;
}
.item:nth-child(4)::v-deep .card-value {
  font-size: 4.6vmin;
}
.item:nth-child(5)::v-deep .card-value {
  font-size: 4.6vmin;
}

.falseItem {
  margin: 0;
  padding: 0;
  width: calc(100% - 0px);
  /* Dois itens por linha, com espaço entre eles */
}
.falseItem:nth-child(1)::v-deep .card-value {
  font-size: 5.6vmin;
}
.falseItem:nth-child(2)::v-deep .card-value {
  font-size: 4vmin;
}
.falseItem:nth-child(3)::v-deep .card-value {
  font-size: 4vmin;
}
.falseItem:nth-child(2),
.falseItem:nth-child(3) {
  width: calc(50% - 10px);
}

@media (max-width: 760px) {
  .container {
    padding: 10px;
  }
  .container-card {
    display: flex;
    flex-direction: column;
    gap: 20px;
    width: 100%;
  }
  .item:nth-child(1) {
    width: calc(100% - 14px);
  }
  .item:nth-child(3),
  .item:nth-child(4),
  .item:nth-child(5) {
    width: calc(50% - 14px);
  }
}
</style>
