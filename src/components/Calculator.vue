<template>
  <div class="calculator">
    
    <div class="display">
      <div class="answer">
      <!-- {{ current || "Ans = 0" }} -->
      </div>
       <div class="answer">
      {{ answer || "Ans" }}
      </div>
      <div class="calculation">
      {{calculation || 0}}
      </div>
    </div>
    
    <a-button class="dark-grey-button zero"> <span style="margin-right:35px"> Rad </span>  <span style="color: #8e9095">|  </span><span style="margin-left:35px ; color: #8e9095">Deg</span></a-button>
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
      current: "Ans = 0",
      answer: "Ans",
      calculation: "",
      operator: null,
      previous: null,
      operatorClicked: false,
    };
  },
  methods: {
    clear() {
      this.current = "";
      this.answer = "";
      this.calculation = "";
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
      this.calculation = this.calculation +  " " + number;
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
      this.calculation = this.calculation + " " + "÷";
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    times() {
      this.calculation = this.calculation + " " + "x";
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus() {
      this.calculation = this.calculation + " " + "-";
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    plus() {
      this.calculation = this.calculation + " " + "+";
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.previous),
        parseFloat(this.current)
      )}`;
      this.answer = "Ans = " + this.current
      this.previous = null;
    },
  },
  mounted: function () {
   this.current = "";
      this.answer = "";
      this.calculation = "";
}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.answer {
  font-size: 14px;
  color: #8e9095;
  margin-top: 8px;
}
.calculation {
    margin-top: -9px;
    margin-bottom: -6px;
    padding: 0;
    font-size: 36px;
}
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
  background-color: white;
  color: black;
  text-align: right;
   border: 2px solid #9dbee8;
   border-radius: 10px;
   padding-right: 10px;
   margin-bottom: 8px;
}

.zero {
  grid-column: 1/3;
}

.btn {
  background-color: #eee;
  border: 1px solid #eee;
  cursor: pointer;
  font-weight: 400;
}

.dark-grey-button {
  background-color: #dbdce0;
  border: 1px solid #dbdce0;
  color: #202124;
  cursor: pointer;
  margin: 3px;
  font-weight: 400;
  font-family: arial, sans-serif;
  font-size: 13px;
   height: 37px; 
}

.dark-grey-button:hover{
   background-color: #dbdce0;
  border: 1px solid #dbdce0;
  color: #202124;
   height: 37px;
}

.light-grey-button {
  background-color: #f2f3f5;
  border: 1px solid #f2f3f5;
  color: black;
  cursor: pointer;
  margin: 3px;
  font-weight: 400;
  font-family: arial, sans-serif;
  font-size: 13px;
  height: 37px;
  
}

.light-grey-button:hover{
   background-color: #f2f3f5;
   border: 1px solid #f2f3f5;
   color: black;
}
.light-grey-button::selection{
   background-color: #f2f3f5;
   border: 1px solid #f2f3f5;
   color: black;
}

.blue-button:hover{
   border: 1px solid #4286f5;
   color: white;
    background-color: #4286f5;
}

.blue-button {
  background-color: #4286f5;
  border: 1px solid #4286f5;
  color: white;
  cursor: pointer;
  margin: 3px;
   font-family: arial, sans-serif;
  font-size: 13px;
   height: 37px;
}

.btn:active {
  transform: scale(0.95);
}

.operator {
  color: white;
  background-color: orange;
}
</style>
