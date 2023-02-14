<template>
  <main>
    <p>{{ labelVisual }}</p>
    <h1>{{ amountCurrency }}</h1>
    <div class="graphic">
      <slot name="graphic"></slot>
    </div>
    <div class="action">
      <slot name="action"></slot>
    </div>
  </main>
</template>

<script>
const currencyFormater = new Intl.NumberFormat("es-VE", {
  style: "currency",
  currency: "VES",
});
export default {
  props: {
    totalLabel: {
      type: String,
    },
    label: {
      type: String,
      default: null,
    },
    totalAmount: {
      type: Number,
    },
    amount: {
      type: Number,
      default: null,
    },
  },
  computed: {
    amountVisual() {
      return this.amount !== null ? this.amount : this.totalAmount;
    },
    labelVisual() {
      return this.amount !== null ? this.amount : this.totalLabel;
    },
    amountCurrency() {
      return currencyFormater.format(this.amountVisual);
    },
  },
};
</script>

<style scoped>
main {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 100%;
}
h1,
p {
  margin: 0;
  text-align: center;
  color: #181818;
}
h1 {
  margin-top: 14px;
  color: #16ff00;
}
.graphic {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  padding: 48px 24px;
  box-sizing: border-box;
}
</style>

