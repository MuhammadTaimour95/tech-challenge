<template>
  <div class="calculator">
    <div class="display">{{ current || 0 }}</div>
    <a-button class="dark-grey-button zero"> Rad | Deg</a-button>
    <a-button class="dark-grey-button"> x! </a-button>
    <a-button class="dark-grey-button"> ( </a-button>
    <a-button class="dark-grey-button"> ) </a-button>
    <a-button class="dark-grey-button" @click="percentage"> % </a-button>
    <a-button class="dark-grey-button" @click="clear">CE</a-button>
     <a-button class="dark-grey-button"> Inv </a-button>
    <a-button class="dark-grey-button"> sin </a-button>
    <a-button class="dark-grey-button"> ln </a-button>
    <a-button class="light-grey-button" @click="append('7')">7</a-button>
    <a-button class="light-grey-button" @click="append('8')">8</a-button>
    <a-button class="light-grey-button" @click="append('9')">9</a-button>
    <a-button class="dark-grey-button" @click="divide">÷</a-button>
     <a-button class="dark-grey-button"> π </a-button>
    <a-button class="dark-grey-button"> cos </a-button>
    <a-button class="dark-grey-button"> log </a-button>
    <a-button class="light-grey-button" @click="append('4')">4</a-button>
    <a-button class="light-grey-button" @click="append('5')">5</a-button>
    <a-button class="light-grey-button" @click="append('6')">6</a-button>
    <a-button class="dark-grey-button" @click="times">x</a-button>
     <a-button class="dark-grey-button"> e </a-button>
    <a-button class="dark-grey-button"> tan </a-button>
    <a-button class="dark-grey-button"> √ </a-button>
    <a-button class="light-grey-button" @click="append('1')">1</a-button>
    <a-button class="light-grey-button" @click="append('2')">2</a-button>
    <a-button class="light-grey-button" @click="append('3')">3</a-button>
    <a-button class="dark-grey-button" @click="minus">-</a-button>
     <a-button class="dark-grey-button"> Ans </a-button>
    <a-button class="dark-grey-button"> EXP </a-button>
    <a-button class="dark-grey-button"> x<sup>y</sup> </a-button>
    <a-button class="light-grey-button" @click="append('0')">0</a-button>
    <a-button class="light-grey-button" @click="dot">.</a-button>
    <a-button class="blue-button" @click="equal">=</a-button>
    <a-button class="dark-grey-button" @click="plus">+</a-button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: "0",
      operator: null,
      previous: null,
      operatorClicked: false,
    };
  },
  methods: {
    clear() {
      this.current = "";
    },
    sign() {
      this.current =
        this.current.charAt(0) === "-"
          ? this.current.slice(1)
          : `-${this.current}`;
    },
    percentage() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if (this.current.indexOf(".") === -1) {
        this.append(".");
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    times() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    plus() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.previous),
        parseFloat(this.current)
      )}`;
      this.previous = null;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  width: 700px;
  margin: 0 auto;
  grid-template-columns: repeat(7, 1fr);
  grid-auto-rows: minmax(50px, auto);
  display: grid;
  font-size: 40px;
}

.display {
  grid-column: 1/8;
  background-color: #333;
  color: white;
  text-align: right;
}

.zero {
  grid-column: 1/3;
}

.btn {
  background-color: #eee;
  border: 1px solid #eee;
  cursor: pointer;
}

.dark-grey-button {
  background-color: #dbdce0;
  border: 1px solid #dbdce0;
  color: black;
  cursor: pointer;
  margin: 3px;
}

.light-grey-button {
  background-color: #f2f3f5;
  border: 1px solid #f2f3f5;
  color: black;
  cursor: pointer;
  margin: 3px;
}

.blue-button {
  background-color: #4286f5;
  border: 1px solid #4286f5;
  color: white;
  cursor: pointer;
  margin: 3px;
}

.btn:active {
  transform: scale(0.95);
}

.operator {
  color: white;
  background-color: orange;
}
</style>
