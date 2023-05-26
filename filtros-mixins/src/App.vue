<!-- Mixins e Filtros são formatações de visualização -->

<template>
  <div id="app">
    <h1>Filtros e Mixins</h1>
    <hr>
    <p>{{ cpf | inverter | formataCPF }}</p>
    <hr>
    <h2>Frutas</h2>
    <ul>
      <li v-for="fruta in frutas" :key="fruta">
        {{ fruta }}
      </li>
    </ul>
    <input type="text" v-model="fruta" @keydown.enter="add" />
    <hr>
    <novofrutas />
  </div>
</template>

<script>

//Importando um mixin, porém dos componentes :)
import Novofrutas from './components/NovoFrutas.vue';
import frutas from './mixins/frutas';




export default {
  components: { Novofrutas },
  mixins: [frutas],
  filters: {
    formataCPF(valor) {
      const array0 = valor.split('');
      array0.splice(3, 0, '.');
      array0.splice(7, 0, '.');
      array0.splice(11, 0, '.');
      return array0.join('');
    },
    inverter(valor) {
      return valor.split('').reverse().join('');
    }
  },
  data() {
    return {
      cpf: '12345678910',
    }
  },

  methods: {
    add() {
      this.frutas.push(this.fruta);
      this.fruta = '';
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  font-size: 2.5rem;
}

input {
  font-size: 2.5rem;

}
</style>