<template>
  <div class="calculator">
    <h1>Vue Calculator</h1>
    <div class="display">{{ current }}</div>
    <div class="buttons">
      <button @click="clear">C</button>
      <button @click="appendValue('/')">/</button>
      <button @click="appendValue('*')">*</button>
      <button @click="deleteLast">DEL</button>

      <button v-for="num in [7, 8, 9]" :key="num" @click="appendValue(num)">
        {{ num }}
      </button>
      <button @click="appendValue('-')">-</button>

      <button v-for="num in [4, 5, 6]" :key="num" @click="appendValue(num)">
        {{ num }}
      </button>
      <button @click="appendValue('+')">+</button>

      <button v-for="num in [1, 2, 3]" :key="num" @click="appendValue(num)">
        {{ num }}
      </button>
      <button class="equals" @click="calculate">=</button>

      <button @click="appendValue(0)">0</button>
      <button @click="appendValue('.')">.</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: "0",
    };
  },
  methods: {
    appendValue(value) {
      if (this.current === "0" && !isNaN(value)) {
        this.current = value.toString();
      } else {
        this.current += value.toString();
      }
    },
    clear() {
      this.current = "0";
    },
    deleteLast() {
      this.current = this.current.slice(0, -1) || "0";
    },
    calculate() {
      try {
        this.current = eval(this.current).toString();
      } catch (e) {
        this.current = "Error";
      }
    },
  },
};
</script>

<style scoped>
.calculator {
  max-width: 300px;
  margin: 50px auto;
  padding: 20px;
  background-color: #f9f9f9;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  font-family: Arial, sans-serif;
}

h1 {
  text-align: center;
  color: #4caf50;
}

.display {
  font-size: 2rem;
  text-align: right;
  margin-bottom: 10px;
  padding: 10px;
  background-color: #e0e0e0;
  color: #000;
  border-radius: 4px;
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
}

button {
  padding: 15px;
  font-size: 1.2rem;
  color: white;
  background-color: #4caf50;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #45a049;
}

button.equals {
  grid-column: span 2;
  background-color: #ff9800;
}

button.equals:hover {
  background-color: #e68900;
}
</style>
