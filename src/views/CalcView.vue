<template>
  <main>
    <div class="main_title">
      <h1>Calculatrice</h1>
    </div>
    <div class="wrapper">
      <div class="cal">
        <div class="cal_screen col-100">
          <div class="cal_screen-result">{{ showToScreen }}</div>
        </div>
        <div class="cal_keyboard col-100">
          <div id="(" class="cal_key key_function" @click="presskey('(')">
            (
          </div>
          <div id=")" class="cal_key key_function" @click="presskey(')')">
            )
          </div>
          <div
            id="return"
            class="cal_key key_function"
            @click="presskey('return')"
          >
            &lt;
          </div>
          <div id="AC" class="cal_key key_special" @click="presskey('AC')">
            AC
          </div>
          <div id="7" class="cal_key" @click="presskey('7')">7</div>
          <div id="8" class="cal_key" @click="presskey('8')">8</div>
          <div id="9" class="cal_key" @click="presskey('9')">9</div>

          <div id="+" class="cal_key key_function" @click="presskey('+')">
            +
          </div>

          <div id="4" class="cal_key" @click="presskey('4')">4</div>
          <div id="5" class="cal_key" @click="presskey('5')">5</div>
          <div id="6" class="cal_key" @click="presskey('6')">6</div>
          <div id="-" class="cal_key key_function" @click="presskey('-')">
            -
          </div>

          <div id="1" class="cal_key" @click="presskey('1')">1</div>
          <div id="2" class="cal_key" @click="presskey('2')">2</div>
          <div id="3" class="cal_key" @click="presskey('3')">3</div>
          <div id="/" class="cal_key key_function" @click="presskey('/')">
            /
          </div>

          <div id="." class="cal_key" @click="presskey('.')">.</div>
          <div id="0" class="cal_key" @click="presskey('0')">0</div>
          <div id="=" class="cal_key key_function" @click="presskey('=')">
            =
          </div>
          <div id="*" class="cal_key key_function" @click="presskey('*')">
            *
          </div>
        </div>
      </div>
      <div class="lastResult">
        <div class="lastResult-title">
          <h2>Derniers résultats</h2>
        </div>
        <div class="lastResult-values">
          <div v-for="(row, index) in lastResult" v-bind:key="index">
            {{ row.expression }} = {{ row.value }}
            <hr v-if="index !== lastResult.length - 1" />
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      showToScreen: "0",
      egalPress: false,
      lastResult: [],
      lastExpression: [],
    };
  },
  methods: {
    presskey(value) {
      let key = document.getElementById(value);
      key.classList.add("key_pressed");
      setTimeout(() => key.classList.remove("key_pressed"), 150);
      if (this.egalPress) {
        console.log(this.egalPress);
        this.showToScreen = value;
        this.egalPress = false;
      } else if (this.showToScreen === "0" || this.showToScreen == "") {
        this.showToScreen = value;
      } else if (value === "=") {
        console.log("egal");
        try {
          let expression = this.showToScreen;
          let result = eval(this.showToScreen).toString();
          this.lastResult.push({
            expression: expression,
            value: result,
          });
          console.log(this.lastResult);
          this.egalPress = true;
        } catch (error) {
          console.log(error);
        }
      } else if (value === "AC") {
        this.showToScreen = "0";
      } else if (value === "return") {
        this.showToScreen = this.showToScreen.slice(0, -1);
        if (this.showToScreen == "") {
          this.showToScreen = "0";
        }
      } else {
        this.showToScreen += value;
      }
    },
  },
  mounted() {
    document.addEventListener("keyup", (event) => {
      switch (event.key) {
        case "0":
        case "1":
        case "2":
        case "3":
        case "4":
        case "5":
        case "6":
        case "7":
        case "8":
        case "9":
        case "+":
        case "-":
        case "*":
        case "/":
        case ".":
        case "(":
        case ")":
          this.presskey(event.key);
          break;
        case "=":
        case "Enter":
          this.presskey("=");
          break;
        case "Backspace":
          this.presskey("return");
          break;
        case "Escape":
          this.presskey("AC");
          if (this.showToScreen == "AC") {
            this.showToScreen = "0";
          }
          break;
        default:
          break;
      }
    });
  },
};
</script>

<style>
.wrapper {
  display: flex;
  flex-wrap: wrap;
  gap: 100px;
  justify-content: space-around;
}

hr {
  margin: 0;
}

.lastResult {
  flex-basis: 50%;
  margin-bottom: 50px;
}

.lastResult-title {
  background-color: var(--second-color);
  text-align: center;
}

.lastResult-values {
  background-color: var(--main-white_color);
  color: var(--main-dark_color);
  font-size: 1.5em;
  line-height: 2em;
  padding: 10px 20px;
  align-self: center;
}
.col-3 {
  flex-basis: 33%;
}

.col-100 {
  flex-basis: 100%;
}

.cal {
  width: 400px;
  border: solid 1px var(--second-color);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 10px;
  padding: 20px 0;
  border-radius: 10px;
}

.cal_screen {
  border: solid 1px var(--second-color);
  border-radius: 5px;
}

.cal_screen-result {
  height: 100px;
  width: 370px;
  border-radius: 3px;
  margin: 2px;
  background-color: var(--main-white_color);
  color: var(--main-dark_color);
  padding: 10px;
  font-size: 2em;
}

.cal_keyboard {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  margin: 10px;
  align-items: center;
  gap: 15px;
}

.cal_key {
  padding: 40px;
  border: solid 1px var(--second-color);
  width: 25px;
  height: 25px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 5px;
  transition: background-color 0.3s ease;
  font-size: 2em;
}

.empty {
  padding: 50px;
  width: 50px;
  height: 50px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 2em;
}

.cal_key:hover {
  background-color: var(--main-color);
}

.key_function {
  background-color: var(--second-color);
}

.key_special {
  background-color: var(--dynamic-color);
}

.key_pressed {
  background-color: var(--light-color);
}
</style>
