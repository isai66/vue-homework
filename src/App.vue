<template>
  <div>
    <h1>Cifrado de Escítala Isaí Lara</h1>
    <label for="message">Ingrese el texto:</label> <br>
    <input type="text" v-model="message" /><br>
    <label for="key">Numero de columnas:</label> <br>
    <input type="number" v-model="key" /> <br>
    <button @click="cifrate">Cifrar</button>
    <div id="result">
      <p>Matriz:</p>
      <table>
        <tr v-for="row in matriz">
          <td v-for="cell in row">{{cell}}</td>
        </tr>
      </table>
      <p v-if="resultadoCifrado">Cifrado: {{ resultadoCifrado }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: "",
      key: 0,
      matriz: [],
      resultadoCifrado: "",
    };
  },
  methods: {
    cifrate() {
      let message = this.message;
      let key = this.key;
      let result = '';
      let matriz = [];

      for (let i = 0; i < Math.ceil(message.length/key); i++) {
        matriz.push([]);
        for (let j=0;j<key;j++) {
          matriz[i].push(' ');
        }
      }
      let cont = 0;

      for (let i=0;i<Math.ceil(message.length/key); i++) {
        for (let j = 0; j < key; j++) {
          matriz[i][j] = message[cont] || ' ';
          cont++;
        }
      }

      for (let i = 0; i < key; i++) {
        for (let j = 0; j < Math.ceil(message.length / key); j++) {
          if (matriz[j][i] !== ' ') {
            result += matriz[j][i];
          } else {
            result += ' ';
          }
        }
      }
      this.matriz = matriz;
      this.resultadoCifrado = result;
    },
  },
};
</script>