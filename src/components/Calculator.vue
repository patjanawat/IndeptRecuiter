<template>
  <div class="calculator">
    <div class="display">{{screen}}</div>
    <div @click="append(0)" class="button  number">0</div>
    <div @click="append(1)" class="button number">1</div>
    <div @click="append(2)" class="button number">2</div>
    <div @click="append(3)" class="button number">3</div>
    <div @click="append(4)" class="button number">4</div>
    <div @click="append(5)" class="button number">5</div>
    <div @click="add" class="button operator">+</div>
    <div @click="subtract" class="button operator">-</div>
    <div @click="multiply" class="button operator">x</div>
    <div @click="divide" class="button operator">÷</div>
    <div @click="equal" class="button equal">=</div>  
    <div @click='clear' class='button darker clear'>C</div>
  </div>
</template>

<script>
export default {
  name:'Calculator',
  data() {
    return {
      previous: null,
      display: 0,
      operator: null,
      operatorClicked: false,
      screen:'',
      symbol:'',
      number:0,
      isEqualClicked:false
    };
  },
  methods:{
    clear() {
      this.display = 0;
      this.screen=''      
    },
     append(number) {
       if(this.isEqualClicked===true){
         this.screen=''  
         this.isEqualClicked = !this.isEqualClicked
       }

      if (this.operatorClicked === true) {
        this.display = ''      
        this.operatorClicked = false;
      }
      this.display =
        this.display === 0
          ? (this.display = number)
          : '' + this.display + number;  
      
      this.content(number)
                
    },
    content(value){
      this.screen = this.screen + `${value}`      
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.previous = this.display;
      this.operatorClicked = true;   
      
      this.content('/')
    },
    multiply() {
      this.operator = (a, b) => a * b;
      this.previous = this.display;
      this.operatorClicked = true;
      this.content('X')
    },
    subtract() {
      this.operator = (a, b) => a - b;
      this.previous = this.display;
      this.operatorClicked = true;
      this.content('-')
    },
    add() {
      this.operator = (a, b) => a + b;
      this.previous = this.display;
      this.operatorClicked = true;
      this.content('+')
    },
    equal() {    
      this.display = this.operator(Number(this.previous), Number(this.display));
      this.previous = null;
      this.operatorClicked = true;

      this.isEqualClicked = !this.isEqualClicked 
      this.content(this.display === 0?'':`=${this.display}`)      
      
    }
  } 
}
</script>

<style scoped>
.calculator {
  margin: auto;
  width: 17vw;
  font-size: 2rem;
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  grid-auto-rows: minmax(10vh, auto);
  border: 5px solid #111;
  line-height: 10vh;
}

.display {
  grid-column: 1 / 7;
  background-color: #ccc;
  border: 1px solid #111;
  border-top: 0;
  font-size: 2.5rem;
  cursor: default;
  overflow: hidden;
  text-overflow: ellipsis;
  padding: 0 1rem;
}

.button {
  /* background-color: hsl(0, 0%, 75%); */
  /* border: 1px dotted #111;   */
      padding: 10px;
}

.button:hover {
  cursor: pointer;
  background: #8eb110;;
}

.operator {
  background-color: hsl(73, 60%, 60%);
}

.equal {
  /* grid-column: 5/7; */
  background: #3d733d;
  color: #fff;
}
.equal:hover {
  background-color:hsl(136, 78%, 17%);
}

.number {
  background: #eee
}

.number:hover {
  background: #aaa
}

.darker {
  background-color: hsl(0, 0%, 65%);
}

.clear:hover{
background: #efaa8d;
color:red;
}
</style>
