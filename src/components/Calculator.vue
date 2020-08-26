<template>
  <section class="container">

    <h1>{{ title }}</h1>

    <div class="calculator">
      <input type="text" placeholder="0" @keyup.enter="calc" v-model="result"/>
      <div class="buttons">
        <div class="numbers">
          <button class="cell" @click="backspace">&#8592;</button>
          <button class="cell" v-for="(num, index) in numbers" :key="`num-${index}`" @click="input(num)">{{num}}</button>
        </div>
        <div class="operators">
          <button class="cell calc" @click="calc">=</button>
          <button class="cell" v-for="(op, index) in operators" :key="`op-${index}`" @click="input(op)">{{op}}</button>
        </div>
        <button class="cell reset" @click="reset">C</button>
      </div>
    </div>

  </section>
</template>

<script>
export default {

  data() {

    return {
      title: "Vuejs Calculator App",
      result: "",
      numbers: [')', '(', 9, 8, 7, 6, 5, 4, 3, 2, 1, '', '.', 0],
      operators: ["+", "-", "*", "/"]
    };

  },

  methods: {

    backspace() {
      this.result = this.result.toString().slice(0, -1);
    },

    input(char) {
      this.result === 'Syntax Error' ? this.result = char : this.result += char.toString();
    },

    reset() {
      this.result = "";
    },

    calc() {
      try {
        this.result = eval(this.result);
        if (this.result === undefined) {
          this.reset();
        }
      }
      catch(e) {
        console.log(e.message);
        this.result = 'Syntax Error';
      }
    },

  }

};
</script>

<style lang="scss">
/*Reset*/
html,body,div,span,applet,object,iframe,blockquote,pre,a,abbr,acronym,address,big,cite,code,del,dfn,em,font,img,ins,kbd,q,s,samp,small,strike,strong,sub,sup,tt,var,b,u,i,center,p,h1,h2,h3,h4,h5,h6,dl,dt,dd,ol,ul,li,fieldset,form,legend,table,tbody,tfoot,thead,tr,th{margin:0;padding:0;border:0;outline:0;font-size:100%;vertical-align:baseline;background:transparent}body{line-height:1}ol,ul{list-style:none}blockquote,q{quotes:none}:focus{outline:0}ins{text-decoration:none}del{text-decoration:line-through}table{border-collapse:collapse;border-spacing:0}
/*Reset*/

$color_bg: #fafafa;
$color_text: #000;
$color_shadow: #808080;
$color_bg_calculator: #fff;
$color_bg_cell: #CDCECF;
$color_bg_reset: #d39e00;
$color_bg_calc: #0062cc;

#main {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  font-weight: normal;
  font-style: normal;
  line-height: 1.2;
  background: $color_bg;
  color: $color_text;
  min-height: 100vh;

  .container {

    h1 {
      text-align: center;
      padding: 30px 0;
    }

    .calculator {
      width: 304px;
      padding: 3px;
      margin: 0 auto;
      box-shadow: 0 3px 15px $color_shadow;
      background: $color_bg_calculator;
      border-radius: 8px;

      input[type="text"],
      .cell {
        font-size: 16px;
        background: $color_bg_cell;
        border: 3px solid $color_bg_calculator;
        border-radius: 8px;
      }

      input[type="text"] {
        width: 304px;
        height: 40px;
        box-sizing: border-box;
        text-align: right;
        padding: 0 10px;
      }

      .buttons {
        display: flex;
        position: relative;
        z-index: 1;

        .cell {
          width: 76px;
          height: 40px;
          cursor: pointer;

          &:hover {
            filter: brightness(1.1);
          }

        }

        .numbers {
          width: 228px;
          display: flex;
          flex-wrap: wrap;
          flex-direction: row-reverse;
        }

        .operators {
          display: flex;
          flex-wrap: wrap;
          flex-direction: column-reverse;
        }

        .reset {
          background: $color_bg_reset;
          position: absolute;
          bottom: 0;
          right: 76px;
          z-index: 2;
        }

        .calc {
          background: $color_bg_calc;
        }

      }

    }

  }

}
</style>
