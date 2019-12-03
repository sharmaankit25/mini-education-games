<template>
  <q-page padding>
    <div v-if="start">
      <h3 class="text-h6 q-pa-sm" padding>Points : {{points}}</h3>
    <p class="row">
      <q-input v-if="hiddenNum == 1" label="Enter Number" outlined
        v-model="userInput"
        autofocus
     />
      <span v-else class="text-h6 q-pa-sm" padding>{{ number1 }}</span>

      <span class="text-h6 q-pa-sm">{{ operator }}</span>

      <q-input v-if="hiddenNum == 2" label="Enter Number" outlined
        v-model="userInput"
        autofocus
     />
      <span v-else class="text-h6 q-pa-sm" padding>{{ number2 }}</span>
      <span class="text-h6 q-pa-sm">=</span>

      <q-input v-if="hiddenNum == 3" label="Enter Number" outlined
        v-model="userInput"
        autofocus
      />
      <span v-else class="text-h6 q-pa-sm" padding>{{ number3 }}</span>
    </p>
    </div>

    <q-btn v-if="start" color="info" label="Check" @click="checkAnswer" />
    <br><br>
    <q-btn  v-if="!start" color="primary" label="Start" @click="generate" />
    <q-btn  v-else color="grey" label="Reset" @click="restart" />
  </q-page>
</template>

<script>
// import { Notify } from 'quasar'
export default {
  name: "PageIndex",
  data(){
    return {
      number1:null,
      number2:null,
      number3:null,
      operators: ["+","-"],
      operator:"",
      start:false,
      hiddenNum:null,
      userInput:null,
      points:0
    }
  },
  methods:{
    restart(){
      this.points = 0;
      this.generate()
    },
    generate(){
      this.start = true

      // Set Which part of the number should be hidden
      this.hiddenNum = [1,2,3][Math.floor(Math.random() * 3)]
      this.operator = this.operators[Math.floor(Math.random()*this.operators.length)]

      this.number1 = Math.abs(Math.floor((Math.random() * 10) + 1))
      this.number2 = Math.abs(Math.floor((Math.random() * 10) + 1))
      this.number3 = parseFloat(eval(this.number1 + this.operator + this.number2))
      if(!isFinite(this.number3) && this.number3 < 0){
        this.generate()
      }
    },
    checkAnswer(){

      switch(this.hiddenNum){
        case 1 :
          if(this.userInput == this.number1){
            this.$q.notify({
              color: 'green',
              message: 'Well Done.Correct Answer !'
              })
            this.points += 1
          }else{
            this.$q.notify({
              color: 'red',
              message: 'Oops Incorrect. Try again!'
              })
          }
          break;
        case 2 :
          if(this.userInput == this.number2){
            this.$q.notify({
              color: 'green',
              message: 'Well Done.Correct Answer !'
              })
              this.points += 1
          }else{
            this.$q.notify({
              color: 'red',
              message: 'Oops Incorrect. Try again!'
              })
          }
          break;
        case 3:
          if(this.userInput == this.number3){
            this.$q.notify({
              color: 'green',
              message: 'Well Done.Correct Answer !'
              })
              this.points += 1
          }else{
            this.$q.notify({
              color: 'red',
              message: 'Oops Incorrect. Try again!'
              })
          }
          break;
      }

      this.userInput = null;
      this.generate()
    }
  }
};
</script>
