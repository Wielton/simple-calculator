<template>
  <v-container fluid>
    <v-row class="pa-6">
      <v-col cols="12">
        <v-input disabled outlined height="50" class="calc-display pa-6 d-flex align-center">{{ calculator.displayValue }}</v-input>
      </v-col>
    </v-row>
    <v-row class="ma-auto">
      <v-col cols="3" class="pa-6 d-flex justify-center" v-for="numBtn in calculatorNumbers" :key="numBtn.id">
        <v-btn :numBtn="numBtn" outlined class="num-btn" @click="updateDisplay(numBtn.numName)">{{numBtn.numName}}</v-btn>
      </v-col>
      <v-col cols="3" class="pa-6 d-flex justify-center" v-for="funcBtn in calculatorFunctions" :key="funcBtn.id">
        <v-btn :funcBtn="funcBtn" outlined class="func-btn" :color="funcBtn.btnColor ? funcBtn.btnColor : 'aqua'" @click="keyFunctions(funcBtn.func)">{{funcBtn.funcName}}</v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  export default {
    name: 'HelloWorld',

    data: () => ({
      calculatorNumbers: [
        { id: 1, numName: '1', btnValue: 1 },
        { id: 2, numName: '2', btnValue: 2 },
        { id: 3, numName: '3', btnValue: 3 },
        { id: 4, numName: '4', btnValue: 4  },
        { id: 5, numName: '5', btnValue: 5  },
        { id: 6, numName: '6', btnValue: 6  },
        { id: 7, numName: '7', btnValue: 7  },
        { id: 8, numName: '8', btnValue: 8  },
        { id: 9, numName: '9', btnValue: 9  },
        { id: 10, numName: '0', btnValue: 0 },
      ],
      calculatorFunctions: [
        { id: 11, funcName: '+', btnValue: '+', func: 'add' },
        { id: 12, funcName: '-', btnValue: '-', func: 'subtract' },
        { id: 13, funcName: 'x', btnValue: '*', func: 'multiply' },
        { id: 14, funcName: '/', btnValue: '/', func: 'divide' },
        { id: 15, funcName: 'C', btnValue: 'c', func: 'clearDisplay', btnColor: 'red' },
        { id: 16, funcName: '.', btnValue: '.', func: 'decimal' },
        { id: 17, funcName: '=', btnValue: '=', func: 'solve', btnColor: 'green' },
      ],
      calculator: {
        displayValue: '0',
        firstOperand: null,
        isWaitingForSecondOperand: false,
        operator: null,
        secondOperand: null,
        result: null
      },
    }),
    methods: {
      logEvent(e){
        console.log(e)
      },
      
      clearDisplay(){
        this.calculator.displayValue = '0'
        this.calculator.firstOperand = null
        this.calculator.operator = null
        this.calculator.result = null
      },
      
      // addNumber(item){
      //   if(this.calculator.isWaitingForSecondOperand === false)
      //   this.calculator.firstOperand
      // },
      updateDisplay(item){ 
        if(this.calculator.displayValue === '0'){
          this.calculator.displayValue = item
        }else{
          this.calculator.displayValue += item
        }
      },
      calculate(){
        this.calculator.secondOperand
      },
      adding(num1, num2){
        console.log('Adding...')
        const finalResult = num1 + num2
        return finalResult
      },
      
      subtract(num1, num2){
        console.log('Subtracting...')
        const finalResult = num1 - num2
        return finalResult
      },
      
      multiply(num1, num2){
        console.log('Multiplying...')
        const finalResult = num1 * num2
        return finalResult
      },
      
      divide(num1, num2){
        console.log('Dividing...')
        const finalResult = num1 / num2
        return finalResult
      },
      
      // solve(num1,num2,func){
      //   this.calculatedResult = num1 + func + num2
      //   console.log('Solving...')
      // },
      
      keyFunctions(str){
        if(this.calculator.firstOperand === null){
          this.calculator.firstOperand = parseFloat(this.calculator.displayValue)
        }
          
          if(str == 'add' && this.calculator.operator === null){
            this.calculator.operator = '+'
            this.updateDisplay(this.calculator.operator)
            this.calculator.isWaitingForSecondOperand = true
            this.calculator.displayValue = ''
            console.log(this.calculator)
          }
          else if(str == 'subtract' && this.calculator.operator === null){
            this.calculator.operator = '-'
            this.updateDisplay(this.calculator.operator)
            this.calculator.isWaitingForSecondOperand = true
            this.calculator.displayValue = ''
            console.log(this.calculator)
          }
          else if(str == 'multiply' && this.calculator.operator === null){
            this.calculator.operator = 'x'
            this.updateDisplay(this.calculator.operator)
            this.calculator.isWaitingForSecondOperand = true
            this.calculator.displayValue = ''
            console.log(this.calculator)
          }
          else if(str == 'divide' && this.calculator.operator === null){
            this.calculator.operator = '/'
            this.updateDisplay(this.calculator.operator)
            this.calculator.isWaitingForSecondOperand = true
            this.calculator.displayValue = ''
            console.log(this.calculator)
          }
          else if(str == 'clearDisplay'){
            this.clearDisplay()
          }
          else if(str == 'decimal'){
            if(!this.calculator.displayValue.includes('.')){
              this.updateDisplay('.')
              console.log(this.calculator.displayValue)
            }
            
          }
          else{
            if(this.calculator.firstOperand && this.calculator.operator){
              this.calculator.secondOperand = parseFloat(this.calculator.displayValue)
              if(this.calculator.operator == '+'){
                this.calculator.result = this.calculator.firstOperand + this.calculator.secondOperand
                this.calculator.displayValue = this.calculator.result
              }else if(this.calculator.operator == '-'){
                this.calculator.result = this.calculator.firstOperand - this.calculator.secondOperand
                this.calculator.displayValue = this.calculator.result
              }else if(this.calculator.operator == 'x'){
                this.calculator.result = this.calculator.firstOperand * this.calculator.secondOperand
                this.calculator.displayValue = this.calculator.result
              }else if(this.calculator.operator == '/'){
                this.calculator.result = this.calculator.firstOperand / this.calculator.secondOperand
                this.calculator.displayValue = this.calculator.result
              }else 
              this.clearDisplay()
              // if(this.operator == '+'){
              //   const result = this.adding(firstNum, secNum)
              //   this.displayValue = result
              //   // this.calculatedResult = +this.firstOperand + this.lastOperand
              //   // console.log("Solving...")
              //   // console.log(this.calculatedResult)
              // }
            }
            
          }
        },
      
    }
  }
</script>
<style lang="scss" scoped>
.num-btn.v-btn--outlined {
  border: thin solid aqua;
  color: aqua;
}
.func-btn.v-btn--outlined {
  border: thin solid whitesmoke;
  color: whitesmoke;
}
.calc-display {
  background-color: whitesmoke;
}
</style>