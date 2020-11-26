<template>
  <div id="app">
    <h1 class="text-white text-center p-4 mt-20 ">VueJs Calculator</h1>
    <div class="mybox mt-16 pb-32" >
        <div id="calculator">
        <div id="result">
            <!-- <div id="history">
                <p id="history-value">{{ showDetails }}</p>
            </div> -->
            <div id="output" class="p-1">
                {{current || 0}}
            </div>
        </div>
        <div id="keyboard" class="text-white">
            <div class="row mt-2 text-white pt-4 pl-2" >
                <div class="col-3">
                    <button style="background-color:#989586" class="operator rounded-full text-white" @click="clear">C</button>
                </div>
                <div class="col-3">
                    <button style="background-color:#989586" class="operator text-white rounded-full" @click="sign">+/-</button>
                </div>
                <div class="col-3">
                    <button style="background-color:#989586" class="operator  rounded-full text-white" @click="percent">%</button>
                </div>
                <div class="col-3">
                    <button class="operator bg-orange-dark rounded-full  text-white" @click="add">+</button>
                </div>
            </div>
            <div class="row mt-4 pl-2">
                <div class="col-3">
                    <button @click="append('7')" class="number bg-grey-darkest rounded-full text-white">7</button>
                </div>
                <div class="col-3">
                    <button @click="append('8')" class="number bg-grey-darkest rounded-full text-white">8</button>
                </div>
                <div class="col-3">
                    <button @click="append('9')" class="number bg-grey-darkest rounded-full text-white">9</button>
                </div>
                <div class="col-3">
                    <button  class="operator bg-orange-dark rounded-full text-white " @click="times">x</button>
                </div>
            </div>

            <div class="row mt-4 pl-2">
                <div class="col-3">
                    <button @click="append('4')" class="number bg-grey-darkest rounded-full text-white">4</button>
                </div>
                <div class="col-3">
                    <button @click="append('5')" class="number bg-grey-darkest rounded-full text-white">5</button>
                </div>
                <div class="col-3">
                    <button @click="append('6')" class="number bg-grey-darkest rounded-full text-white">6</button>
                </div>
                <div class="col-3">
                    <button class="operator bg-orange-dark rounded-full text-white" @click="minus">-</button>
                </div>
            </div>

            <div class="row mt-4 pl-2">
                <div class="col-3">
                    <button  @click="append('1')" class="number bg-grey-darkest rounded-full text-white">1</button>
                </div>
                <div class="col-3">
                    <button  @click="append('2')" class="number bg-grey-darkest rounded-full text-white">2</button>
                </div>
                <div class="col-3">
                    <button  @click="append('3')" class="operator number bg-grey-darkest rounded-full text-white">3</button>
                </div>
                <div class="col-3">
                    <button class="operator bg-orange-dark rounded-full text-white" @click="add">+</button>
                </div>
            </div>

            <div class="row mt-4 pl-2">
                <div class="col-3  ">
                    <button  @click="append('0')" class="number bg-grey-darkest rounded-full text-white">0</button>
                </div>
                <div class="col-3 offset-3 ">
                    <button class="operator text-white number bg-grey-darkest rounded-full" @click="dot">.</button>
                </div>
                <div class="col-3  ">
                    <button class="operator bg-orange-dark rounded-full text-white" @click="equal">=</button>
                </div>
            </div>

        </div>
        </div>

    </div>
  </div>
</template>


<script>
export default {
  name: 'App',
  data(){
    return{
        previous: null,
        operatorClicked: false,
        current:'',
        operator:null,
    }
  },
  methods:{
    clear(){
        this.current = '';
    },
     sign: function(){
        return this.current = this.current.charAt(0) === '-' ?
        this.current.slice(1) : `-${this.current}`;
        // this.current = `${-this.current}`;
    },
    percent(){
      this.current = `${parseFloat(this.current)/100}`
    },
   
    append(number){
        if(this.operatorClicked){
            this.current = '';
            this.operatorClicked = false;
        }
        this.current = `${this.current}${number}`;
    },
    dot(){
        if(this.current.indexOf('.') === -1){
            this.append('.');
        }
    },
    // deleteOut(){
    //     // let trans = [];
    //     // trans = this.current;
    //     // trans.pop();
    //     // console.log(trans);
    //     // let digit = Array.from(String(this.current), Number);
       
    //   let trans = this.current.split('').map((item)=>{
    //       return parseInt(item)
    //       });
    //       for(let i = 1; i < trans.length;i++){
    //           trans.pop(i);

    //       }
        
    //      trans.join();
    //     console.log(trans);
    // },
    setPrevious(){
        this.operatorClicked = true;
        this.previous = this.current;
    },
    divide(){
        this.operator = (a,b) => a/b;
        this.setPrevious();
    },
    add(){
        this.operator = (a,b) => a+b;
        this.setPrevious();
    },
    minus(){
        this.operator = (a,b) => b-a;
        this.setPrevious();
    },
    times(){
        this.operator = (a,b) => a*b;
        this.setPrevious();
        
    },
    equal(){
        this.current = `${this.operator(
            parseFloat(this.current),
            parseFloat(this.previous)
            )}`;
            this.previous = null;

    },
    showDetails(){
    this.current;
    },
    // fixSize(){
    //     while(){}
    // }
  
  },
  computed:{ //only use for transforming data or changing presentation of existing data they should not alter change in an existing data
      

  }
}
</script>

<style>
body{
    background-color:  #040f20;
}
.mybox{
    background-color:  #040f20;
}

.number{
    
}
#calculator{
    width: 344px;
    height: 520px;
    background-color: #eaedef;
    margin-left:  auto;
    margin-right: auto;
    top: 20px;
    left: 0px;
    left: 0px;
    right: 0px;
    bottom: 0px; 
    position: relative;
    border-radius: 5px;
    box-shadow: 0px 4px 8px 0 black;
}
#firstCard{
    margin: auto;
    top: 0;
    right: 0;
    left: 0;
    bottom: right;
    display: block;
}
.answer{
    border: 1px solid gray;
    width: 400px;
    display: block;
}
#result{
    height: 120px;
    overflow-x: hidden;
    overflow-y: hidden;
}
#history{
    text-align: right;
    height: 20px;
    margin: 0 20px;
    padding-top: 20px;
    font-size: 15px;
    color: #919191;
    
}
#output{
    float: right;
    height: 60px;
    margin: 10px 20px;
    font-size: 50px;
    
}
#keyboard{
  
    height: 400px;
    background-color:  #040f20;
    font-size: 20px;
    
   
}
button{
    height: 50px;
    width: 50px;
    border-radius: 50%;
    font-weight: bold;
}
.operator,.number{
    cursor: pointer;
}
.operator:focus, .number:focus, .empty:focus{
    outline: 0;
}

.operator:active, .number:active{
    font-size: 12px;
}
button:nth-child(4){
    font-size: 20px;
    background-color: rgb(45, 204, 17);
}


</style>
