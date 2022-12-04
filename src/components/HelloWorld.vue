<template>
  <v-container fluid>
    <v-row class="pa-6">
      <v-col cols="12">
        <v-card outlined height="50" class="pa-6 d-flex align-center">{{ displayValue }}</v-card>
      </v-col>
    </v-row>
    <v-row class="ma-auto">
      <v-col cols="3" class="pa-6 d-flex justify-center">
        <v-btn outlined class="fb-btn" v-model="one" @click="updateDisplay(one)">1</v-btn>
      </v-col>
      <v-col cols="3" class="pa-6 d-flex justify-center">
        <v-btn outlined class="fb-btn" v-model="two" @click="updateDisplay(two)">2</v-btn>
      </v-col>
      <v-col cols="3" class="pa-6 d-flex justify-center">
        <v-btn outlined class="fb-btn" v-model="three" @click="updateDisplay(three)">3</v-btn>
      </v-col>
      <v-col cols="3" class="pa-6 d-flex justify-center">
        <v-btn outlined class="fb-btn" @click="chooseOperator('add')">+</v-btn>
      </v-col>
    </v-row>
    <v-row class="ma-auto">
      <v-col cols="3" class="pa-6 d-flex justify-center">
        <v-btn outlined class="fb-btn" v-model="four" @click="updateDisplay(four)">4</v-btn>
      </v-col>
      <v-col cols="3" class="pa-6 d-flex justify-center">
        <v-btn outlined class="fb-btn" v-model="five" @click="updateDisplay(five)">5</v-btn>
      </v-col>
      <v-col cols="3" class="pa-6 d-flex justify-center">
        <v-btn outlined class="fb-btn" v-model="six" @click="updateDisplay(six)">6</v-btn>
      </v-col>
      <v-col cols="3" class="pa-6 d-flex justify-center">
        <v-btn outlined class="fb-btn">-</v-btn>
    </v-col>
    </v-row>
    <v-row class="ma-auto">
      <v-col cols="3" class="pa-6 d-flex justify-center">
        <v-btn outlined class="fb-btn" v-model="seven" @click="updateDisplay(seven)">7</v-btn>
      </v-col>
      <v-col cols="3" class="pa-6 d-flex justify-center">
        <v-btn outlined class="fb-btn" v-model="eight" @click="updateDisplay(eight)">8</v-btn>
      </v-col>
      <v-col cols="3" class="pa-6 d-flex justify-center">
        <v-btn outlined class="fb-btn" v-model="nine" @click="updateDisplay(nine)">9</v-btn>
      </v-col>
      <v-col cols="3" class="pa-6 d-flex justify-center">
        <v-btn outlined class="fb-btn">x</v-btn>
      </v-col>
    </v-row>
    <v-row class="ma-auto">
      <v-col cols="3" class="pa-6 d-flex justify-center" >
        <v-btn outlined class="fb-btn" @click="clear">C</v-btn>
      </v-col>
      <v-col cols="3" class="pa-6 d-flex justify-center">
          <v-btn outlined class="fb-btn" v-model="zero" @click="updateDisplay(zero)">0</v-btn>
      </v-col>
      <v-col cols="3" class="pa-6 d-flex justify-center">
          <v-btn outlined class="fb-btn">=</v-btn>
      </v-col>
      <v-col cols="3" class="pa-6 d-flex justify-center">
          <v-btn outlined class="fb-btn">/</v-btn>
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
      waitingForSecondOperand: false,
      operator: null,
      one: 1,
      two: 2,
      three: 3,
      four: 4,
      five: 5,
      six: 6,
      seven: 7,
      eight: 8,
      nine: 9,
      zero: 0,
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
      clear(){this.displayValue = ''},
      appendNum(num){ this.firstOperand= num },
      chooseOperator(operation){ 
        this.firstOperand = this.displayValue 
        if(operation == 'add'){
          this.operator = '+'
        }else if(operation == 'subtract'){
          this.operator = '-'
        }else if(operation == 'multiply'){
          this.operator = '*'
        }else{
          this.operator = '/'
        }
        this.displayValue = this.firstOperand + this.operator
        console.log("Your equation so far is: " + this.firstOperand + ' ' + this.operator)
      },
      compute(){},
      updateDisplay(item){ 
        this.displayValue += item
        }
    }
  }
</script>
<style lang="scss" scoped>
.fb-btn.v-btn--outlined {
  border: thin solid aqua;
  color: aqua;
}
</style>