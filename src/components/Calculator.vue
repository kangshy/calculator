<template>
  <div>
      <button class="operator plus" @click="operator">+</button>
      <button class="operator minus" @click="operator">-</button>
      <button class="operator multiple" @click="operator">×</button>
      <button class="operator division" @click="operator">÷</button>
      <br>
      <button class="number" @click="setvalue">7</button>
      <button class="number" @click="setvalue">8</button>
      <button class="number" @click="setvalue">9</button>
      <button class="backspace"><img src="@/img/backspace.jpg" @click="remove"></button>
      <br>
      <button class="number" @click="setvalue">4</button>
      <button class="number" @click="setvalue">5</button>
      <button class="number" @click="setvalue">6</button>
      <button class="clear" @click="initAll">C</button>
      <br>
      <button class="number" @click="setvalue">1</button>
      <button class="number" @click="setvalue">2</button>
      <button class="number" @click="setvalue">3</button>
      <button class="operator equal" @click="calculate">=</button>
      <br>
      <button class="number" @click="setvalue">0</button>
  </div>
</template>

<script>
import { mapMutations } from 'vuex'

export default {
    data() {
        return {
            inputdata : '',
            done:false,
            isSetOperator:false,
        }
    },
    methods: {
        ...mapMutations(['initState']),
        ...mapMutations(['setExp']),
        ...mapMutations(['fixExp']),
        ...mapMutations(['setNum1']),
        ...mapMutations(['setNum2']),
        ...mapMutations(['setOperator']),
        ...mapMutations(['setResult']),

        initAll() {
            this.inputdata='';
            this.done=false;
            this.isSetOperator=false;
            this.initState();
        },

        setvalue(e){
            if(this.done){
                this.initState();
                this.done=false;
            }
            this.inputdata+=e.target.innerText;
            this.setExp(e.target.innerText);
        },
        operator(e) {
            if (this.isSetOperator) {
                alert('이미 연산자를 선택하였습니다.');
            } else if(this.inputdata.length==0) {
                alert('숫자를 먼저 입력하세요');
            } else {
                this.setNum1(this.inputdata);
                this.setExp(e.target.innerText);
                this.setOperator(e.target.innerText);
                this.inputdata='';
                this.isSetOperator=true;
            }
        },
        calculate(e) {
            this.setNum2(this.inputdata);
            this.setExp(e.target.innerText);
            this.setResult();
            this.done=true;
            this.isSetOperator=false;
            this.inputdata='';
        },
        remove() {
            this.inputdata=this.inputdata.slice(0, this.inputdata.length-1);
            this.fixExp();
        },
    },
}
</script>

<style>
button
{
    width : 60px;
    height : 60px;
    border : 0;
    margin : 5px;
}

.number
{
    background-color : #cdcdcd;
    font-size : 17px;
}

.operator
{
    font-size:23px;
}

.plus
{
    background-color : #E8F5E9;
}
.minus
{
    background-color : #F0F4C3;
}
.multiple
{
    background-color : #FBE9E7;
}
.division
{
    background-color : #E8EAF6;
}
.equal
{
    background-color : #BBDEFB;
}
</style>