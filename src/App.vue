<template>
  <div id="app">
    <input v-model="inputN" type="number" placeholder="N" />
    <input v-model="inputK" type="number" placeholder="K" />
    <button @click="calculate(Number(inputN), Number(inputK))">
      Calculate
    </button>
    <p v-show="result != null">n! = {{ this.factorial(n) }}</p>
    <p v-show="result != null">y! = {{ this.factorial(k) }}</p>
    <p v-show="result != null">
      {{ this.factorial(n) }} / {{ this.factorial(k) }}( {{ n }} - {{ k }} ) =
      {{ result }}
    </p>
    <p v-show="result != null">
      Le coeficient binomial est de : {{ binomial }}
    </p>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      inputK: "",
      inputN: "",
      n: "",
      k: "",
      result: null,
      binomial: null,
    };
  },
  methods: {
    calculate(n, k) {
      this.n = n;
      this.k = k;
      this.inputK = "";
      this.inputN = "";
      if (n > k && k >= 0) {
        const coeficient = this.coef(n, k);
        const divideFacto =
          this.factorial(this.n) / (this.factorial(this.k) * (n - k));
        const result = divideFacto;
        this.binomial = coeficient;
        return (this.result = result);
      } else {
        return (this.result = 0);
      }
    },
    pascals(numRows) {
      if (numRows === 0) return [];
      if (numRows === 1) return [[1]];
      let result = [];
      for (let row = 1; row <= numRows + 1; row++) {
        let arr = [];
        for (let col = 0; col < row; col++) {
          if (col === 0 || col === row - 1) {
            arr.push(1);
          } else {
            arr.push(result[row - 2][col - 1] + result[row - 2][col]);
          }
        }
        result.push(arr);
      }
      return result;
    },
    coef(n, k) {
      const arr = this.pascals(n);
      const binomial = arr[n][k];
      return binomial;
    },
    factorial(n) {
      let answer = 1;
      if (n === 0 || n === 1) {
        return answer;
      } else {
        for (var i = n; i >= 1; i--) {
          answer = answer * i;
        }
        return answer;
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
input {
  width: 90px;
}
</style>
