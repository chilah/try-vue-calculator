<template>
  <div id="app">
    <p>PreviousValue: {{previousValue ? previousValue : 0}}</p>
    <p>Operation: {{operation}}</p>
    <p>CurrentValue: {{currentValue ? currentValue : 0}}</p>
    <p>Length: {{currentValue.length}}/8</p>
    <p>Result: {{result}}</p>
    <button @click="addValue('1')">1</button>
    <button @click="addValue('2')">2</button>
    <button @click="addValue('3')">3</button>
    <button @click="addOperation('+')">+</button>
    <button @click="deleteCurrentValue">Delete</button>
    <button @click="resultValue">=</button>
    <button @click="clearAll">Clear</button>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      currentValue: "",
      previousValue: "",
      operation: "",
      result: 0
    };
  },
  methods: {
    addValue(value) {
      if (this.currentValue.length < 8) {
        this.currentValue += value;
      }
    },
    addOperation(value) {
      this.operation = value;

      if (!this.previousValue) {
        this.previousValue = this.currentValue;
        this.currentValue = "";
      }

      if (this.previousValue && this.currentValue) {
        this.resultValue();
        this.previousValue = this.result;
        this.currentValue = "";
      }
    },
    resultValue() {
      const { previousValue, currentValue } = this;
      const previousNumber = parseInt(previousValue, 10);
      const currentNumber = parseInt(currentValue, 10);

      if (this.operation === "+") {
        this.result = previousNumber + currentNumber;
      }
    },
    deleteCurrentValue() {
      this.currentValue = this.currentValue.slice(
        0,
        this.currentValue.length - 1
      );
    },
    clearAll() {
      this.currentValue = "";
      this.previousValue = "";
      this.operation = "";
      this.result = 0;
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
