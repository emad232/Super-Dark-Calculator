<template>
  <div class="calculator card">



    <div class="calculator-screen">

    

      <input type="text" readonly class="form-control-plaintext text-light text-center" v-model="formattedTnput" />
      <div class="funcScreen"> 
        {{showFunc}}
      </div>
    </div>


    <div class="calculator-function">
      <button type="button" value="clear-all" class="btn mybtn mybtn-fun mybtn-ac" @click="clearAll()">
        AC
      </button>
      <button type="button" value="/" class="btn mybtn mybtn-fun mybtn-primary2" @click="startFunc('/')">
        /
      </button>
      <button type="button" value="*" class="btn mybtn mybtn-fun mybtn-primary2" @click="startFunc('*')">
        *
      </button>
      <button type="button" value="+" class="btn mybtn mybtn-fun mybtn-primary2" @click="startFunc('+')">
        +
      </button>
      <button type="button" value="-" class="btn mybtn mybtn-fun mybtn-primary2" @click="startFunc('-')">
        -
      </button>
    </div>
    <div class="calculator-keys">
      <button type="button" value="7" class="btn mybtn" @click="addToInput('7')">
        7
      </button>
      <button type="button" value="8" class="btn mybtn" @click="addToInput('8')">
        8
      </button>
      <button type="button" value="9" class="btn mybtn" @click="addToInput('9')">
        9
      </button>

      <button type="button" value="4" class="btn mybtn" @click="addToInput('4')">
        4
      </button>
      <button type="button" value="5" class="btn mybtn" @click="addToInput('5')">
        5
      </button>
      <button type="button" value="6" class="btn mybtn" @click="addToInput('6')">
        6
      </button>

      <button type="button" value="1" class="btn mybtn" @click="addToInput('1')">
        1
      </button>
      <button type="button" value="2" class="btn mybtn" @click="addToInput('2')">
        2
      </button>
      <button type="button" value="3" class="btn mybtn" @click="addToInput('3')">
        3
      </button>

      <button type="button" class="btn mybtn " :class="{                                                                                                                                                                                                                  mybtnFunActive: (dec)                                                                                                                                                                                                                  }" @click="addDecimal()">.</button>
      <button type="button" value="0" class="btn mybtn" @click="addToInput('0')">
        0
      </button>
      <button type="button" class="btn mybtn mybtn-primary" @click="endFunc()">=</button>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import "bootstrap/dist/css/bootstrap.min.css";

export default defineComponent({
  name: "myNum",

  data() {
    return {
      input: '0',
      dec: false,
      lastInput: 0,
      myFunc: ''
      // inputF: ''
    };
  },
  methods: {
    async addToInput(num: string) {

      if ((this.input.toString().length) < 9) {

        if (this.dec == true) {





          this.input = (String(this.input) + "." + num);
          this.dec = false
        } else {
        //todo 0 problem
        if (((this.input).startsWith('0')) && (num == '0') && (!this.input.includes('.'))) {
          this.input = '0';
        } else {
          if (((this.input).startsWith('0')) && (num != '0') && (!this.input.includes('.'))) {
            this.input = num;
          }else{
                      this.input = (String(this.input) + num);

          }

        }
///end PB

        }

      }

    },
    async addDecimal() {
      if (Number(this.input) == Math.floor(Number(this.input))) {
        this.dec = (!(this.dec))
      } else {
        this.dec = false
      }
    },
    async clearAll() {
      this.input = '0';
      this.lastInput = 0
    },
    async startFunc(Func: string) {
      this.lastInput = Number(this.input);
      this.input = '0';
      this.myFunc = Func
    },
    async endFunc() {
      // const funStr= String(this.lastInput)+this.myFunc+this.input ;
      const addition = Function("a", "b", "return a" + this.myFunc + "b")
      const fun = addition(this.lastInput, Number(this.input));
      this.input=String(fun)
      // console.log(fun)

    }
  },
  props: {
    name: String,
  },
  computed: {

    formattedTnput: {
      get() {

        // let decZero = String(this.input);
        // if(this.input0==true){
        //   decZero='0';
        //   this.input0=false
        // }
        const result1 = this.input

        const finalresult = result1.replace(/\B(?=(\d{3})+(?!\d))/g, " ");


        return finalresult;
      },
      set(value: string | number) {
        ((this.input) = this.input + value);
      },
    },
    showFunc() {
      if((this.myFunc)!=""){
      const show = String(this.lastInput)+" "+this.myFunc

      return show
      }else{
        return null;
      }
    }
  },
});
</script>

<style scoped>
.calculator {
  border: 1px solid #ccc;
  border-radius: 5px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 100%;
  height: 100vh;
}

.calculator-screen {
  width: 100%;
  height: 100%;
  background-color: #191b1d;
  color: #fff;
  text-align: center;
  padding: 30px;
  font-size: 3.5rem !important;
  padding-bottom: 0px;
}

button {
  /* height: 60px; */
  font-size: 2rem !important;
}

.calculator-keys {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  /* grid-gap: 5px;
      padding: 20px; */
  /* height: 0vh; */
  background: #191b1d;
  /* bottom: 0px; */
  margin-bottom: 0px;
}

.mybtn {
  background: #1e2022;
  color: #ffffff;
  font-weight: 300;
  padding: 15%;
  border: 0.5px solid #191b1d;
  border-radius: 0px !important;
}

.mybtn-primary {
  background: #1939f6 !important;
}

.mybtn-primary2 {
  background: #0047ab !important;
}

.mybtn-ac {
  background: #097969 !important;
}

.mybtn-fun {
  width: 20%;
  padding: 10px;
}

.calculator-function {
  display: flex;
  flex-direction: row;
  background: #191b1d;
}

.mybtnFunActive {
  background: #666600;
  opacity: 50%;
}
.funcScreen {
  /* height: 25px; */
  min-height: 30px;
  min-width: 40px;
  font-size: 15px;
  position: fixed;
  top: 0px;
  left: 0px;
  margin: 10px;
  background: #EE4B2B;
  padding: 5px;
  padding-left: 10px;
  padding-right: 10px;
  border-radius: 40px;
}
body{
  background-color: #191b1d;

}
</style>
