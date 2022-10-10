<template>
  <div class="flex flex-col md:flex-row justify-center">
    <div class="flex flex-col w-4/5 md:w-auto border-2 h-auto rounded-xl p-3 bg-gray-50 shadow-xl mt-10">
      <Display :expValue="displayValue" dispType="expr"/>
      <Display :expValue="resultValue" dispType="result"/>
      <div v-show="isError" class="text-center bg-red-400 my-5 rounded-xl">
        <p>Please check the expression</p>
      </div>
      <div class="grid grid-cols-4 gap-3">
        <CalcButton 
          v-for="(val, index) in rows" 
          :key="index" 
          :buttonValue="val" 
          @on-click="updateExpression(val)"
        />
      </div>
    </div>
    <History :historyList="historyList" @historyClick="onHistoryItemClick" />
  </div>
</template>

<script>

import Display from './components/Display.vue';
import CalcButton from './components/CalcButtons.vue';
import History from './components/History.vue';

export default {
  name: 'App',
  components: {
    Display,
    CalcButton,
    History
  },
  data() {
    return {
      rows: [
        "AC", "DEL", "%", "/", 
        "7", "8", "9", "*", 
        "4", "5", "6", "-", 
        "1", "2", "3", "+", 
        "0", ".", "="
      ],
      expression: "",
      isError: false,
      result: "",
      historyList: []
    }
  },
  computed: {
    displayValue() {
      if (this.expression === "") {
        return "0";
      } else {
        return this.expression;
      }
    },
    resultValue() {
      if (this.result === "") {
        return "0";
      } else {
        return this.result;
      }
    },
  },
  methods: {
    updateExpression(buttonValue) {
      if (buttonValue == "AC") {
        this.isError = false;
        this.expression = "";
        this.result = "";
      } else if (buttonValue == "DEL") {
        this.isError = false;
        this.expression = this.expression.slice(0, -1);
      } else if (buttonValue === "=") {
        try {
          let res = Function(`"use strict"; return ${this.expression};`)();
          console.log(res);
          this.result = String(res);
        } catch(e) {
          this.isError = true;
        }
        this.historyList.push({
          expr: this.expression,
          result: this.result
        })
      } else if (isNaN(buttonValue)) {
        if (isNaN(this.expression.slice(-1))){
          this.isError = true;
        }
        else if (this.result !== "") {
          this.expression = this.result + buttonValue;
        } else {
          this.expression += buttonValue;
        }
      } else {
        if (this.result !== "") {
          this.expression = "";
          this.result = "";
        }
        this.isError = false;
        this.expression += buttonValue;
      }
    },
    onHistoryItemClick(index) {
      // console.log(index);
      this.expression = this.historyList[index].result;
      this.result = "";
    }
  }
}
</script>