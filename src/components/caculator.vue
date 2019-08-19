<template>
  <div class="caculator">
    <div class="display">{{ crt || '0' }}</div>
    <div class="ctr">
      <ul>
        <li @click="clear">C</li>
        <li @click="sign">+/-</li>
        <li @click="percent">%</li>
        <li @click="divide">/</li>
      </ul>
      <ul>
        <li @click="append(7)">7</li>
        <li @click="append(8)">8</li>
        <li @click="append(9)">9</li>
        <li @click="times">X</li>
      </ul>
      <ul>
        <li @click="append(4)">4</li>
        <li @click="append(5)">5</li>
        <li @click="append(6)">6</li>
        <li @click="minus">-</li>
      </ul>
      <li>
        <li @click="append(1)">1</li>
        <li @click="append(2)">2</li>
        <li @click="append(3)">3</li>
        <li @click="add">+</li>
      </li>
      <ul>
        <li @click="back">bk</li>
        <li @click="append(0)">0</li>
        <li @click="dot">.</li>
        <li @click="equal">=</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "caculator",
  data() {
    return {
      crt: "",
      previous: null,
      operator: null,
      operatorClicked: false
    };
  },
  methods: {
    clear() {
      this.crt = "";
    },
    sign() {
      this.crt =
        this.crt.charAt(0) === "-" ? this.crt.slice(1) : `-${this.crt}`;
    },
    percent() {
      this.crt = `${parseFloat(this.crt) / 100}`;
      //this.crt = parseFloat(this.crt) / 100;
    },
    append(i) {
      if (this.operatorClicked) {
        this.crt = "";
        this.operatorClicked = false;
      }
      this.crt = `${this.crt}${i}`;
    },
    back() {},
    dot() {
      if (this.crt.indexOf(".") === -1) {
        this.append(".");
      }
    },
    setPrevious() {
      this.previous = this.crt;
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
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {
      this.crt = `${this.operator(
        parseFloat(this.previous),
        parseFloat(this.crt)
      )}`;
      console.log(parseFloat(this.crt)); //-3
      console.log(parseFloat(this.previous)); //9
      console.log(this.crt);
      this.previous = null;
    }
  }
};
</script>

<style scoped lang="sass">
$blue: #fff;

ul
  list-style: none
  margin: 0
  padding: 0
  display: flex
  li
    width: 25%
    height: 100px
    line-height: 100px
    border: 1px solid rgba(135,124,121,0.2)
    cursor: point
    transition: all 0.3s
    &:hover
      background-color: rgba(255,255,255,0.2)
      border: 1px solid rgba(255,255,255,0.2)
      font-size: 2.5rem
      font-weight: bold
    

.caculator 
  color: $blue
  position: absolute
  top: 50%
  left: 50%
  transform: translate(-50%,-50%)
  width: 400px
  //height: 800px
  box-shadow: 8px 8px 40px rgba(35,24,21,1)
  transition: all 0.5s
  &:hover
    transform: translate(-51%,-51%)
    box-shadow: 20px 20px 50px rgba(35,24,21,1)


.display
  height: 200px
  line-height: 200px
  font-size: 4rem
  text-align: right
  padding: 0 0.8rem 
  overflow: hidden
  border-bottom: 1px solid rgba(255,255,255,0.3)
  background: linear-gradient(171deg, #fc473b 51%, #e5394c 79%)
  background: -moz-linear-gradient(171deg, #fc473b 51%, #e5394c 79%)
  background: -webkit-linear-gradient(171deg, #fc473b 51%, #e5394c 79%)
  background: -o-linear-gradient(171deg, #fc473b 51%, #e5394c 79%)

.ctr
  background: linear-gradient(180deg, #e04f64 0%, #9d3081 100%)
  background: -moz-linear-gradient(180deg, #e04f64 0%, #9d3081 100%)
  background: -webkit-linear-gradient(180deg, #e04f64 0%, #9d3081 100%)
  background: -o-linear-gradient(180deg, #e04f64 0%, #9d3081 100%)

</style>
