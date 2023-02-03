<template>
  <div id="app">
    <img class="img" src="./assets/cronometro.png" alt="a" />
    <a class="timer">{{ number }}</a>
    <div class="areabtn">
      <button class="button" @click="vai">{{ botao }}</button>
      <button class="button" @click="limpar">LIMPAR</button>
    </div>

    <div class="list" v-show="historico.length > 0">
      <ul>
        <li v-for="item in historico" :key="item">
          VOCÊ FEZ UMA PAUSA EM: {{ item }}
        </li>
      </ul>
      <button class="buttonhist" @click="limparHist">Limpar historico</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      number: "00:00,00",
      botao: "VAI",
      timer: null,
      ss: 0,
      mm: 0,
      hh: 0,
      historico: [],
    };
  },
  methods: {
    vai() {
      if (this.timer !== null) {
        clearInterval(this.timer);
        this.timer = null;
        this.botao = "VAI";
        this.historico.push(this.number);
      } else {
        this.timer = setInterval(() => {
          this.rodarTimer();
        }, 10);
        this.botao = "PAUSAR";
      }
    },
    limpar() {
      if (this.timer !== null) {
        clearInterval(this.timer);
        this.timer = null;
      }
      this.ss = 0;
      this.mm = 0;
      this.hh = 0;
      this.number = "00:00,00";
      this.botao = "VAI";
      this.historico = [];
    },
    rodarTimer() {
      this.ss++;

      if (this.ss == 59) {
        this.ss = 0;
        this.mm++;
      } else if (this.mm == 59) {
        this.mm = 0;
        this.hh++;
      }

      // eslint-disable-next-line prettier/prettier
      let format = (this.hh < 10 ? "0" + this.hh : this.hh) + ":"
        // eslint-disable-next-line prettier/prettier
      +(this.mm < 10 ? "0" + this.mm : this.mm) + ","
        // eslint-disable-next-line prettier/prettier
      +(this.ss < 10 ? "0" + this.ss : this.ss);
      return (this.number = format);
    },
    limparHist() {
      return (this.historico = []);
    },
  },
};
</script>

<style>
#app {
  display: flex;
  width: 100%;
  height: 100vh;
  align-items: center;
  flex-direction: column;
}
.img {
  width: 420px;
  height: 420px;
  margin-top: 150px;
}
.timer {
  color: #fff;
  font-size: 70px;
  margin-top: -240px;
}
.areabtn {
  margin-top: 155px;
  display: flex;
}
.button {
  width: 150px;
  background-color: #fff;
  font-size: 20px;
  border: 0;
  border-radius: 5px;
  text-align: center;
  margin: 0 15px;
  padding: 6px;
  cursor: pointer;
}
.button:hover {
  opacity: 0.8;
  transition: all 0.5s;
}
ul {
  text-align: center;
  padding: 0px;
}

ul li {
  margin-top: 4px;
  padding: 15px;
  background-color: rgb(70, 70, 70);
  list-style: none;
  font-size: 18px;
  border-radius: 15px;
}
.buttonhist {
  background-color: #fff;
  font-size: 12px;
  border: 0;
  border-radius: 5px;
  margin-top: 5px;
  text-align: center;
  padding: 6px 20px;
  cursor: pointer;
}
</style>
