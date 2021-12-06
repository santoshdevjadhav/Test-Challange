<template>
  <div class="main-wrapper">
    <div class="custom-input">
      <div class="wrapper-class">
        <img src="../assets/timer.png" alt="" />
        <div class="ans" v-if="answer.length !== 0">Ans = {{ finalAnswer }}</div>
      </div>
      <div class="result-wrapper">{{ finalExpression }}</div>
    </div>
    <div class="custom-switch-wrapper">
      <div class="col-1">
        <div class="row-1">
          <button class="large-btn">
            Rad <span class="pipe">|</span> <span class="deg">Deg</span>
          </button>
          <button class="gray-btn">x!</button>
        </div>
        <div class="row-2">
          <button class="gray-btn">lnv</button>
          <button class="gray-btn">sin</button>
          <button class="gray-btn">ln</button>
        </div>
        <div class="row-2">
          <button class="gray-btn text-md">ℼ</button>
          <button class="gray-btn">cos</button>
          <button class="gray-btn">log</button>
        </div>

        <div class="row-2">
          <button class="gray-btn text-md">e</button>
          <button class="gray-btn">tan</button>
          <button class="gray-btn text-md">√</button>
        </div>

        <div class="row-2">
          <button class="gray-btn">Ans</button>
          <button class="gray-btn">EXP</button>
          <button class="gray-btn">X<sup>y</sup></button>
        </div>
      </div>
      <div class="col-2">
        <div class="row-2">
          <button class="gray-btn">(</button>
          <button class="gray-btn">)</button>
          <button class="gray-btn">%</button>
        </div>
        <div class="row-3">
          <button
            v-for="n in ['7', '8', '9']"
            :key="n"
            type="button"
            :value="n"
            @click.stop="buttonClick"
            class="gray-light-btn"
          >
            {{ n }}
          </button>
        </div>

        <div class="row-3">
          <button
            v-for="n in ['4', '5', '6']"
            :key="n"
            type="button"
            :value="n"
            @click.stop="buttonClick"
            class="gray-light-btn"
          >
            {{ n }}
          </button>
        </div>

        <div class="row-3">
          <button
            v-for="n in ['1', '2', '3']"
            :key="n"
            type="button"
            :value="n"
            @click.stop="buttonClick"
            class="gray-light-btn"
          >
            {{ n }}
          </button>
        </div>

        <div class="row-3">
          <button
            v-for="n in ['0', '.']"
            :key="n"
            type="button"
            :value="n"
            @click.stop="buttonClick"
            class="gray-light-btn"
          >
            {{ n }}
          </button>
          <button
            type="button"
            @click.prevent="calculate"
            class="gray-blue-btn"
          >
            &#x3d;
          </button>
        </div>
      </div>
      <div class="col-3">
        <div class="row-4">
          <button type="button" @click.prevent="clearResult" class="gray-btn">
            CE
          </button>
          <button
            type="button"
            value="/"
            @click.stop="buttonClick"
            class="gray-btn text-md"
          >
            &#xf7;
          </button>
          <button
            type="button"
            value="*"
            @click.stop="buttonClick"
            class="gray-btn"
          >
            &#x2716;
          </button>
          <button
            type="button"
            value="-"
            @click.stop="buttonClick"
            class="gray-btn"
          >
            &#x268A;
          </button>
          <button
            type="button"
            value="+"
            @click.stop="buttonClick"
            class="gray-btn"
          >
            &#x271A;
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { evaluate } from "mathjs";
export default {
  name: "calculator",
  data() {
    return {
      expression: '',
      answer: '',
    };
  },
  computed: {
    finalExpression() {
      return this.expression || '';
    },
    finalAnswer() {
      return this.answer || '';
    },
    lastDigit() {
      return this.expression.slice(-1);
    }
  },
  methods: {
    calculate() {
      if (this.lastDigit !== ' ') this.answer = evaluate(this.expression);
    },
    buttonClick(event) {
      const value = event.target.value;
      if (!isNaN(value) || value === '.') {
        this.expression += `${value}`;
      } else {
        if (!isNaN(this.lastDigit) && this.lastDigit !== ' ') this.expression += ` ${value} `;
      }
    },
    clearResult() {
      this.expression = '';
      this.answer = '';
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@500&display=swap");
button {
  font-weight: 600;
  cursor: pointer;
}
.text-md {
  font-size: 20px;
}

.result-wrapper {
  line-height: 40px;
  text-align: right;
  width: 100%;
  height: 40px;
  display: flex;
  font-size: 32px;
  justify-content: flex-end;
}
.ans {
  color: #a7a6a4;
}
.wrapper-class {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  padding: 8px 5px 0;
}
.wrapper-class img {
  cursor: pointer;
  width: 18px;
  min-width: 18px;
  height: 18px;
}
.main-wrapper {
  max-width: 800px;
  font-family: "Roboto", sans-serif;
  margin: 0 auto;
}
.custom-input {
  height: 60px;
  border: 2px solid #95b3e5;
  border-radius: 8px;
  position: relative;
  margin-bottom: 12px;
  padding: 5px 10px;
  box-shadow: inset 1px 2px 3px 0px rgba(0, 0, 0, 0.10);
}
.custom-switch-wrapper {
  display: flex;
  gap: 10px;
}
.col-3 {
  gap: 10px;
  display: flex;
  flex: 1;
  flex-direction: column;
}
.col-1,
.col-2 {
  gap: 10px;
  display: flex;
  flex: 3;
  flex-direction: column;
}
.row-4 {
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.row-1,
.row-2,
.row-3 {
  display: flex;
  gap: 10px;
}
.custom-input input {
  border: none;
  width: 98%;
  text-align: right;
  line-height: 40px;
  font-size: 24px;
  position: absolute;
  bottom: 0;
  outline: none;
}
.large-btn {
  border-radius: 6px;
  flex: 2.3;
  line-height: 40px;
  height: 40px;
  font-size: 16px;
  background: #dbdce0;
  color: #1f2024;
  border: none;
  display: flex;
  justify-content: space-evenly;
  align-items: center;
}
.large-btn:hover {
  background: #dbdce0c4;
}
.large-btn .pipe {
  color: #84878c;
  margin: 5px;
}
.large-btn .deg {
  color: #84878c;
}
.gray-blue-btn {
  background: #4286f5;
  color: #fff;
  font-weight: bold;
  font-size: 16px;
  flex: 1;
  border-radius: 6px;
  line-height: 40px;
  border: none;
}
.gray-blue-btn:hover {
  background: #4286f5c9;
}
.gray-light-btn {
  background: #f2f3f5;
  color: #1f2024;
  font-size: 16px;
  flex: 1;
  border-radius: 6px;
  line-height: 40px;
  border: none;
}
.gray-light-btn:hover {
  background: #e9eef9;
}
.gray-btn:hover {
  background: #dbdce0cf;
}
.gray-btn {
  border: none;
  flex: 1;
  line-height: 40px;
  background: #dbdce0;
  color: #1f2024;
  border-radius: 6px;
  position: relative;
}
.gray-btn sup {
  position: absolute;
  top: -7px;
}
</style>
