<template>
  <q-page padding>
    <div v-if="start">
    <p class="row">
      <my-input :value.sync="number1" />
      <span class="text-h6 q-pa-sm">{{ operator }}</span>
      <my-input :value.sync="number2" />
      <span class="text-h6 q-pa-sm">=</span>
      <my-input :value.sync="number3" />
    </p>
    </div>
    <q-btn v-if="start" color="info" label="Check" @click="checkAnswer" />
    <br><br>
    <q-btn color="primary" label="Generate" @click="generate" />
  </q-page>
</template>

<script>
import MyInput from '../components/MyInput'
export default {
  name: "PageIndex",
  data(){
    return {
      number1:null,
      number2:null,
      number3:null,
      operators: ["*","+","-","/"],
      operator:"",
      start:false,
      hiddenNum:null,
      userInput:null
    }
  },
  methods:{
    generate(){
      this.start = true

      // Set Which part of the number should be hidden
      this.hiddenNum = [1,2,3][Math.floor(Math.random() * 3)]
      this.operator = this.operators[Math.floor(Math.random()*this.operators.length)]

      this.number1 = this.hiddenNum != 1 ?  Math.abs(Math.floor((Math.random() * 10) + 1)) : null
      this.number2 = this.hiddenNum != 2 ?  Math.abs(Math.floor((Math.random() * 10) + 1)) : null
      this.number3 = this.hiddenNum != 3 ? parseFloat(eval(this.number1 + this.operator + this.number2)) : null
      if(!isFinite(this.number3)){
        this.generate()
      }
    },
    checkAnswer(){
      switch(this.hiddenNum){
        case 1 :
          alert(1)
          break;
        case 2 :
          alert(2)
          break;
        case 3:
          alert(this.number3)
          break;
      }
    }
  },
  components: {
    MyInput
  }
};
</script>
