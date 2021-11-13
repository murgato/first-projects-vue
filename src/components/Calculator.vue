<template id='Container'>
  <div class="Container-Calculator">
    <span> Calculator</span>
    <div class="Panel">
      <span class="secondary">{{ painelSecondary }} </span>
      <span class="primary">{{ primary }}</span>
    </div>
    <div class="Container-Button">
      <div>
        <button v-on:click="limpar">C</button>
        <button v-on:click="sinal">+/-</button>
        <button v-on:click="porcentagem">%</button>
        <button v-on:click="setOperador('-')">-</button>
      </div>
      <div>
        <button v-on:click="adicionarNumero(1)">1</button>
        <button v-on:click="adicionarNumero(2)">2</button>
        <button v-on:click="adicionarNumero(3)">3</button>
        <button v-on:click="setOperador('+')">+</button>
      </div>
      <div>
        <button v-on:click="adicionarNumero(4)">4</button>
        <button v-on:click="adicionarNumero(5)">5</button>
        <button v-on:click="adicionarNumero(6)">6</button>
        <button v-on:click="setOperador('÷')">÷</button>
      </div>
      <div>
        <button v-on:click="adicionarNumero(7)">7</button>
        <button v-on:click="adicionarNumero(8)">8</button>
        <button v-on:click="adicionarNumero(9)">9</button>
        <button v-on:click="setOperador('x')">X</button>
      </div>
      <div>
        <button class="Btn-zero" v-on:click="adicionarNumero(0)">0</button>
        <button v-on:click="adcionarPonto()">.</button>
        <button v-on:click="efetuarOperacao">=</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  data() {
    return {
      painelSecondary: "",
      secondary: "",
      primary: "",
      operador: "",
      operadorClicado: false,
    };
  },
  methods: {
    limpar() {
      this.painelSecondary = "";
      this.secondary = "";
      this.primary = "";
      this.operadorClicado = false;
    },
    sinal() {
      this.primary =
        this.primary.charAt(0) === "-"
          ? this.primary.slice(1)
          : `-${this.primary}`;
    },
    porcentagem() {
      this.primary = `${parseFloat(this.primary) / 100}`;
    },
    adicionarNumero(numero) {
      this.primary += numero;
    },
    adcionarPonto() {
      if (this.primary.indexOf(".") === -1) {
        this.adicionarNumero(".");
      }
    },
    setOperador(operador) {
      if (!this.operadorClicado) {
        this.operador = operador;
        this.operadorClicado = !this.operadorClicado;
        this.painelSecondary = this.primary + " " + operador;
        this.secondary = this.primary;
        this.primary = "";
      }
    },
    efetuarOperacao() {
      if (this.operadorClicado) {
        console.log(this.operador);
        var valor;
        switch (this.operador) {
          case "+":
            valor = Number(this.primary) + Number(this.secondary);
            console.log(this.primary, this.secondary);
            this.painelSecondary += " " + this.primary;
            this.primary = valor.toString();
            this.operadorClicado = false;
            break;
          case "-":
            valor = Number(this.secondary) - Number(this.primary);
            this.painelSecondary += " " + this.primary;
            this.primary = valor.toString();
            this.operadorClicado = false;
            break;
          case "x":
            valor = Number(this.primary) * Number(this.secondary);
            console.log(valor);
            this.painelSecondary += " " + this.primary;
            this.primary = valor.toString();
            this.operadorClicado = false;
            break;
          case "÷":
            valor = Number(this.secondary) / Number(this.primary);
            this.painelSecondary += " " + this.primary;
            this.primary = valor.toString();
            this.operadorClicado = false;
            break;
          default:
            break;
        }
      }
    },
  },
};
</script>
<style scoped>
div.Container-Calculator {
  display: flex;
  flex-direction: column;
  align-content: center;
  justify-content: center;
  align-items: center;
}
div.Container-Button {
  display: flex;
  flex-direction: column;
}
button.Btn-zero {
  width: 10vh;
}
div.Panel {
  width: 12rem;
  min-height: 5rem;
  border: 1px solid #000;
  margin-bottom: 0.2%;
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  justify-content: flex-end;
}
span.primary {
  font-size: 37px;
  min-height: 3rem;
}

span.secondary {
  font-size: 24px;
}

button {
  height: 5vh;
  width: 5vh;
  font-size: 2vh;
  font-weight: bolder;
}
</style>