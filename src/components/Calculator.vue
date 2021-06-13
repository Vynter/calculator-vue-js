<template>
  <div class="calculator">
    <div class="resultat">{{ current || 0 }}</div>
    <div @click="clear" class="btn">AC</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn ope">/</div>
    <div @click="append(7)" class="btn">7</div>
    <div @click="append(8)" class="btn">8</div>
    <div @click="append(9)" class="btn">9</div>
    <div @click="times" class="btn ope">x</div>
    <div @click="append(4)" class="btn">4</div>
    <div @click="append(5)" class="btn">5</div>
    <div @click="append(6)" class="btn">6</div>
    <div @click="minus" class=" ope">-</div>
    <div @click="append(1)" class="btn">1</div>
    <div @click="append(2)" class="btn">2</div>
    <div @click="append(3)" class="btn">3</div>
    <div @click="plus" class="btn ope">+</div>
    <div @click="append(0)" class="zero btn">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn ope">=</div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  data() {
    return {
      current: "",
      operator: null,
      operatorClicked: false,
      previousValue: null,
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
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(nbr) {
      //   this.current = this.current + nbr;
      //2eme solution
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      this.current = `${this.current}${nbr}`;
    },
    dot() {
      if (this.current.indexOf(".") === -1 && this.current !== "") {
        // si le point n'éxiste pas then do

        this.append(".");
        // or         this.current = `${this.current}.`;
      }
    },
    plus() {
      this.operator = (a, b) => a + b;
      this.previousValue = this.current;
      this.operatorClicked = true;
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.previousValue = this.current;
      this.operatorClicked = true;
    },
    times() {
      this.operator = (a, b) => a * b;
      this.previousValue = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.previousValue = this.current;
      this.operatorClicked = true;
    },
    equal() {
      this.current = this.operator(
        parseFloat(this.previousValue),
        parseFloat(this.current)
      );
      this.previousValue = null;
    },
  },
};
</script>

<style scoped>
.calculator {
  width: 400px;
  font-size: 40px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}

.resultat {
  grid-column: 1/5;
  background: #333;
  color: white;
}

.zero {
  grid-column: 1/3;
  background: red;
}

.btn {
  background: #f2f2f2;
  border: 1px solid #999;
}

.ope {
  background: orange;
}
</style>
