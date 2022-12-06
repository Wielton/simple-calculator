<template>
  <v-container fluid>
    <v-row class="pa-6">
      <v-col cols="12">
        <v-card outlined height="50" class="pa-6 d-flex align-center">{{ displayValue }}</v-card>
      </v-col>
    </v-row>
    <v-row class="ma-auto">
      <v-col cols="3" class="pa-6 d-flex justify-center" v-for="numBtn in calculatorNumbers" :key="numBtn.id">
        <v-btn :numBtn="numBtn" outlined class="num-btn" @click="updateDisplay(numBtn.btnValue); addNumber(numBtn.btnValue)">{{numBtn.numName}}</v-btn>
      </v-col>
      <v-col cols="3" class="pa-6 d-flex justify-center" v-for="funcBtn in calculatorFunctions" :key="funcBtn.id">
        <v-btn :funcBtn="funcBtn" outlined class="func-btn" :color="funcBtn.btnColor ? funcBtn.btnColor : 'aqua'" @click="chooseFunction(funcBtn.func)">{{funcBtn.funcName}}</v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  export default {
    name: 'HelloWorld',

    data: () => ({
      displayValue: '',
      firstOperand: null,
      secondOperand: null,
      isWaitingForSecondOperand: true,
      operator: null,
      calculatedResult: null,
      calculatorNumbers: [
        { id: 1, numName: '1', btnValue: 1 },
        { id: 2, numName: '2', btnValue: 2 },
        { id: 3, numName: '3', btnValue: 3 },
        { id: 4, numName: '4', btnValue: 4 },
        { id: 5, numName: '5', btnValue: 5 },
        { id: 6, numName: '6', btnValue: 6 },
        { id: 7, numName: '7', btnValue: 7 },
        { id: 8, numName: '8', btnValue: 8 },
        { id: 9, numName: '9', btnValue: 9 },
        { id: 10, numName: '0', btnValue: 0 },
      ],
      calculatorFunctions: [
        { id: 11, funcName: '+', btnValue: '+', func: 'add' },
        { id: 12, funcName: '-', btnValue: '-', func: 'subtract' },
        { id: 13, funcName: 'x', btnValue: '*', func: 'multiply' },
        { id: 14, funcName: '/', btnValue: '/', func: 'divide' },
        { id: 15, funcName: 'C', btnValue: 'c', func: 'clearDisplay', btnColor: 'red' },
        { id: 16, funcName: '.', btnValue: '.' },
        { id: 17, funcName: '=', btnValue: '=', func: 'solve', btnColor: 'green' },
      ]
    }),
    methods: {
      logEvent(e){
        console.log(e)
      },
      // Have an empty array to hold the equation so that the data types are retained
      // Have a function to add the given value from the corresponding button to the equation calculator: {
      //                                                                                                    firstOperand: null,
      //                                                                                                    waitingForSecondOperand: false,
      //                                                                                                    operator: null
      //                                                                                                  }
      // I should make an instance of a calculator to track the values instead of tracking individually like it is
      clearDisplay(){this.displayValue = ''},
      
      adding(){console.log('Adding...')},
      
      subtract(){console.log('Subtracting...')},
      
      multiply(){console.log('Multiplying...')},
      
      divide(){console.log('Dividing...')},
      
      // solve(num1,num2,func){
      //   this.calculatedResult = num1 + func + num2
      //   console.log('Solving...')
      // },
      
      chooseFunction(str){
          this.firstOperand = +this.displayValue
          
          if(str == 'add' && this.operator === null){
            this.adding()
            this.operator = '+'
            this.updateDisplay(this.operator)
            console.log("Your equation so far is: " + this.firstOperand + this.operator)
          }else if(str == 'subtract' && this.operator === null){
            this.subtract()
            this.operator = '-'
            this.displayValue = this.firstOperand + this.operator
            console.log("Your equation so far is: " + this.firstOperand + ' ' + this.operator)
          }else if(str == 'multiply' && this.operator === null){
            this.multiply()
            this.operator = '*'
            this.displayValue = this.firstOperand + this.operator
            console.log("Your equation so far is: " + this.firstOperand + ' ' + this.operator)
          }else if(str == 'divide' && this.operator === null){
            this.divide()
            this.operator = '/'
            this.displayValue = this.firstOperand + this.operator
            console.log("Your equation so far is: " + this.firstOperand + ' ' + this.operator)
          }else if(str == 'clearDisplay'){
            this.operator = null
            this.firstOperand = null
            console.log(this.operator, this.firstOperand)
            this.displayValue = ''
          }else if(str == 'decimal'){
            this.displayValue += '.'
          }
          else{
            if(this.firstOperand !== null && this.lastOperand !== null){
              if(this.operator == '+'){
                console.log(this.firstOperand)
                // this.calculatedResult = +this.firstOperand + this.lastOperand
                // console.log("Solving...")
                // console.log(this.calculatedResult)
              }
            }
            
          }
        },
      addNumber(item){
        if(this.operator !== null){
          this.secondOperand = item
          console.log("The second operand: " + this.secondOperand)
        }else{
          this.firstOperand = +this.displayValue
          console.log("The first operand: " + this.firstOperand)
        }
      },
      updateDisplay(item){ 
        this.displayValue += item
        }
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
</style>