<template>
  <main>
    <div class="about">
      <h1>Calculatrice</h1>
    </div>

    <div class="cal">
      <div class="cal_screen col-100">
        <div class="cal_screen-result"> {{ showToScreen }} </div>
      </div>
      <div class="cal_keyboard col-100">
        <div class="cal_key" @click="presskey('return')">&lt;</div>
        <div class="cal_key key_special" @click="presskey('AC')">AC</div>
        <div class="cal_key" @click="presskey('1')">1</div>
        <div class="cal_key" @click="presskey('2')">2</div>
        <div class="cal_key" @click="presskey('3')">3</div>
        <div class="cal_key" @click="presskey('4')">4</div>
        <div class="cal_key" @click="presskey('5')">5</div>
        <div class="cal_key" @click="presskey('6')">6</div>
        <div class="cal_key" @click="presskey('7')">7</div>
        <div class="cal_key" @click="presskey('8')">8</div>
        <div class="cal_key" @click="presskey('9')">9</div>
        <div class="cal_key" @click="presskey('.')">.</div>
        <div class="cal_key" @click="presskey('0')">0</div>
        <div class="cal_key" @click="presskey('+')">+</div>
        <div class="cal_key" @click="presskey('-')">-</div>
        <div class="cal_key" @click="presskey('*')">*</div>
        <div class="cal_key" @click="presskey('/')">/</div>
        <div class="cal_key" @click="presskey('=')">=</div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      showToScreen: '0',
    }
  },
  methods: {
    presskey(value) {
      if (this.showToScreen === '0' || this.showToScreen == '') {
        this.showToScreen = value;
      } else if (value === '=') {
        console.log('egal: ' + this.showToScreen);
        try {
          this.showToScreen = eval(this.showToScreen).toString();
        } catch (error) {

        }
      } else if (value === 'AC') {
        this.showToScreen = "0";
      } else if (value === 'return') {
        this.showToScreen = this.showToScreen.slice(0, -1)
        if (this.showToScreen == '') {
          this.showToScreen = '0';
        }
      } else {

        this.showToScreen += value;
      }
    }
  },
  mounted() {
    document.addEventListener('keyup', (event) => {
      console.log(event);
      switch (event.key) {
        case '0':
        case '1':
        case '2':
        case '3':
        case '4':
        case '5':
        case '6':
        case '7':
        case '8':
        case '9':
        case '+':
        case '-':
        case '*':
        case '/':
        case '.':
          this.presskey(event.key);
          break;
        case '=':
        case 'Enter':
          this.presskey('=');
          break;
        case 'Backspace':
          this.showToScreen = this.showToScreen.slice(0, -1);
          if (this.showToScreen == '') {
            this.showToScreen = '0';
          }
          break;
        case 'Escape':
          this.presskey('AC');
          if (this.showToScreen == 'AC') {
            this.showToScreen = '0';
          }
          break;
        default:
          break;
      }
    });
  },
}
</script>

<style>
.col-3 {
  flex-basis: 33%;
}

.col-100 {
  flex-basis: 100%;
}

.cal {
  width: 350px;
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
  width: 315px;
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
  justify-content: center;
  align-items: center;
  gap: 5px;
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
  transition: background-color .3s ease;
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

.key_special {
  background-color: var(--dynamic-color);
}
</style>
