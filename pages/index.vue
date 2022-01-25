<template>
  <div class="flex-container">
    <article class="flex-item-left">
      <input type="number" v-model="number" @blur="formatNumber()" />
    </article>
    <article class="flex-item-center scroller">
      <select v-model="select">
        <option value="isPrime">isPrime</option>
        <option value="isFibonacci">isFibonacci</option>
      </select>
    </article>
    <article class="flex-item-right">{{ result }}</article>
  </div>
</template>

<script>
export default {
  head() {
    return {
      title: "Section 2-1",
    };
  },
  data() {
    return {
      number: 0,
      select: "isPrime",
      result: "",
      numberChange: true,
    };
  },
  watch: {
    findResult() {
      switch (this.select) {
        case "isPrime":
          this.result = "true";
          for (let i = 2; i < this.number; i++) {
            if (this.number % i == 0) {
              this.result = "false";
            }
          }
          break;
        case "isFibonacci":
          this.result = "false";
          let n1 = 0,
            n2 = 1,
            nextTerm;
          for (let i = 1; n1 <= this.number; i++) {
            if (n1 == this.number) {
              this.result = "true";
            }
            nextTerm = n1 + n2;
            n1 = n2;
            n2 = nextTerm;
          }
          break;
      }
    },
  },
  computed: {
    findResult() {
      return [this.numberChange, this.select];
    },
  },
  methods: {
    formatNumber() {
      this.number < 0
        ? (this.number = 1)
        : (this.number = Math.ceil(this.number));
      this.numberChange = !this.numberChange;
    },
  },
};
</script>

<style scoped>
@media only screen and (max-width: 600px) {
  .scroller {
    width: 300px;
    height: 100px;
    overflow-x: scroll;
    scrollbar-width: thin;
  }
}

.flex-container {
  display: flex;
  font-size: 30px;
  height: 98vh;
}

.flex-item-left {
  min-width: 200px;
}

.flex-item-center {
  width: 100%;
}

.flex-item-right {
  padding-left: 1em;
  min-width: 300px;
}
</style>
