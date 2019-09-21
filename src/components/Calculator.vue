<template>
  <div class="calculator">
    
   <div class="display">{{current||'0'}}</div>
   <div @click="clear" class="option operator">C</div>
   <div @click="sign" class="option operator">+/-</div>
   <div @click="persent" class="option operator">%</div>
   <div @click="divide" class="option operator">÷</div>
   <div @click="append('1')" class="option">1</div>
   <div @click="append('2')" class="option">2</div>
   <div @click="append('3')" class="option">3</div>
   <div @click="times" class="option operator">x</div>
   <div @click="append('4')" class="option">4</div>
   <div @click="append('5')" class="option">5</div>
   <div @click="append('6')" class="option">6</div>
   <div @click="minus" class="option operator">-</div>
   <div @click="append('7')" class="option">7</div>
   <div @click="append('8')" class="option">8</div>
   <div @click="append('9')" class="option">9</div>
   <div @click="plus" class="option operator">+</div>
   <div @click="append('0')" class="option zero"><img src="../assets/Pig.png"></div>
   <div @click="dot" class="option">.</div>
   <div @click="equal" class="option operator">=</div>
  </div>
</template>

<script>
export default {
 data(){
  return{
    previous:null,
    current:'',
    operator:null,
    operatorClicked:false,
  }
 },
 methods: {
   clear(){
   this.current='';
   },
  sign(){
    this.current=this.current.charAt(0)==='-'?
    this.current.slice(1) : `-${this.current}`;
  },
  persent(){
    this.current=`${parseFloat(this.current) / 100}`;

  },
  append(number){
    if(this.operatorClicked)
    {
      this.current='';
      this.operatorClicked=false;
    }
    this.current=`${this.current}${number}`;
  },
  dot(){
    if(this.current.indexOf('.') === -1 ){
      this.append('.');
    }
  },
  setPrevious(){
    this.previous=this.current;
    this.operatorClicked=true;
  },
  divide(){
    this.append('÷') 
    this.operator=(a, b) => a / b;
    this.setPrevious();
  },
  times(){
   
      this.append('*');
    
    this.operator=(a, b) => a * b;
    this.setPrevious();
  },
  minus(){
    this.append('-');
    this.operator=(a, b) => a - b;
    this.setPrevious();
  },
  plus(){
    this.append('+');
    this.operator=(a, b) => a + b;
    this.setPrevious();
  },
  equal(){
   this.current=`${this.operator(
   parseFloat(this.previous),
   parseFloat(this.current),
   )}`;
   this.previous=null;
  }
 }
}
</script>


<style scoped>
.calculator {
  margin:0px auto;
  display:grid;
  font-size: 30px;
  grid-template-columns: repeat(4,1fr);
  grid-auto-rows:minmax(50px,auto);
  line-height:50px;
}
.display{
  grid-column: 1/5;
  background-color:aqua;
  line-height:50px;
}
.zero
{
  grid-column:1/3;
}
.option{
  background-color: white;
  border:1px solid black;
}
.operator{
  background-color:green;
  color:white;
}
</style>
