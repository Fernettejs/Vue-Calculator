<template>
  <div class="calculator">
    <div class="display">{{current || '0'}}</div>
    <div @click="clear" class="btn top-row">C</div>
    <div @click="sign" class="btn top-row">+/-</div>
    <div @click="percent" class="btn top-row">%</div>
    <div @click="divide" class="btn operator">÷</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="multiply" class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="subtract" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator equal">=</div>
  </div>

</template>

<script>
export default {
  data() {
    return {
      previous: null, /* what is this for? */
      current: '',
      operator: null,
      operatorClicked: false, /* what is this for? */
    }
  },
  methods: {
    clear() {
      this.current = '';
    }, 
    sign() {
      this.current = this.current.charAt(0) === '-' ?
        this.current.slice(1) : `-${this.current}` 
  }, 
  percent() {
    this.current = `${parseFloat(this.current) / 100}`
  }, 
  append(number) {
    if (this.operatorClicked) {
      this.current = '';
      this.operatorClicked = false;
    }
    this.current = `${this.current}${number}`;
  }, 
  dot() {
    if (this.current.indexOf('.') === -1) {
      this.append('.');
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
  multiply() {
    this.operator = (a, b) => a * b;
    this.setPrevious();
  },
  subtract() {
    this.operator = (a, b) => a - b;
    this.setPrevious();
  },
  add() {
    this.operator = (a, b) => a + b;
    this.setPrevious();
  },
  equal() {
    this.current = `${this.operator(
      parseFloat(this.current), 
      parseFloat(this.previous)
      )}`;
      this.previous = null; 
  }
}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0; 
  font-family: Helvetica, Arial, sans-serif;


}

.calculator {
  margin: 0 auto;
  width: 235px;
  font-size: 25px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}

.display {
  grid-column: 1 / 5 ;
  background-color: rgb(95, 94, 94);
  color: white;
  padding-top: 25px;
  padding-right: 10px;
  text-align: right;
  font-size: 35px;
  border-top-left-radius: 5px;
  border-top-right-radius: 5px;
  height: 2.0em;
  }

.zero {
  grid-column: 1 / 3;
  border-bottom-left-radius: 5px;

}

.btn {
  padding: 10px;
  background-color: #777777;
  border: 1px solid rgb(63, 63, 63);
  color: white;
  cursor: pointer;
}

.operator {
  background-color: rgb(255, 161, 20);
  color: white;
}

.top-row {
  background-color: rgb(78, 78, 78);
}
.equal {
  border-bottom-right-radius: 5px;
}
</style>
