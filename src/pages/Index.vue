<template>
  <q-page padding>
    <div v-if="start">
    <p class="row">
      <my-input :num="number1" /> <span class="text-h6 q-pa-sm">{{ operator }}</span>  <my-input :num="number2" /> <span class="text-h6 q-pa-sm">=</span> <my-input :num="number3" />
    </p>
    </div>
    <q-btn v-if="start" color="info" label="Check" @click="checkAnswer" />
    <q-btn color="primary" label="Generate" @click="generate" />
  </q-page>
</template>

<script>
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
      hiddenNum:null
    }
  },
  methods:{
    generate(){
      this.start = true

      // Set Which part of the number should be hidden
      this.hiddenNum = [1,2,3][Math.floor(Math.random() * 3)]

      this.number1 = this.hiddenNum != 1 ?  Math.abs(Math.floor((Math.random() * 10) + 1)) : null
      this.number2 = this.hiddenNum != 2 ?  Math.abs(Math.floor((Math.random() * 10) + 1)) : null
      this.operator = this.operators[Math.floor(Math.random()*this.operators.length)]
      this.number3 = this.hiddenNum != 3 ? parseFloat(eval(this.number1 + this.operator + this.number2)) : null
      if(!isFinite(this.number3) || this.number3 <= 0){
        this.generate()
      }
    },
    checkAnswer(){

    }
  },
  components: {
    'my-input': require('components/MyInput.vue').default
  }
};
</script>
