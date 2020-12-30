<template>
  <main>
    <div id="calculator">
      <h1 v-if="result">{{ result }}</h1>
      <h1 v-else>Enter the value</h1>
      <div id="line"></div>
      <div class="buttons">
        <button v-for="num in numbers" @click="add_num(num)" :key="num">{{ num }}</button>
        <button v-for="oper in operators" @click="add_operator(oper)" :key="oper">{{ oper }}</button>
        <button @click="clear">C</button>
        <button @click="dot">.</button>
        <button @click="percent">%</button>
        <button @click="equals" class="equal">=</button>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: 'Calculator',
  data () {
    return {
      result: '',
      numbers: ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9'],
      operators: ['+', '-', '/', '*'],
      operatorClicked: false
    }
  },
  methods: {
    add_num (num) {
      this.add_symbol(num)
      this.operatorClicked = false
    },
    add_symbol (sym) {
      this.result = `${this.result}${sym}`
    },
    add_operator (oper) {
      if (this.operatorClicked == false) {
        this.add_symbol(oper)
      }
      this.operatorClicked = true
    },
    equals () {
      this.result = eval(this.result)
    },
    clear () {
      this.result = ''
    },
    percent () {
      this.result = eval(this.result) / 100
    },
    dot () {
      if (this.result.indexOf('.') === -1) {
        this.add_symbol('.')
      }
    }
  }
}
</script>

<style scoped>
  @import url('https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Space+Mono:wght@400;700&display=swap');
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Share Tech Mono';
    text-align: center;
  }
  .buttons {
    display: grid;
    grid-template-columns: 3fr 3fr 3fr;
    grid-row: 5;
    grid-gap: 10px;
    width: 20em;
  }
  main {
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: 60px;
  }
  button {
    background: #e9f0f4;
    border: 0px solid transparent;
    border-radius: 10px;
    height: 50px;
    font-weight: bold;
    font-size: 18px;
    width: 90px;
  }
  button:focus,button:active {
    border: 0px solid transparent !important;
    outline: none !important;
  }
  .operator {
      background: #f12711;
      background: -webkit-linear-gradient(to right, #f5af19, #f12711);
      background: linear-gradient(to right, #f5af19, #f12711);
  }
  .equal {
    background: #00b09b;
    background: -webkit-linear-gradient(to right, #96c93d, #00b09b);
    background: linear-gradient(to right, #96c93d, #00b09b);
  }
  #line {
    height: 3px;
    background: #999;
    width: 40px;

    margin-left: 136px;
    margin-bottom: 20px;
    margin-top: 20px;
  }
</style>
