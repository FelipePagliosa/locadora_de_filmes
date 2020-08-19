<template>
  <b-container>
    <h1>Bem vindo a {{ title }}</h1>
    <h3 v-if="horas >= 9 && horas < 17" id="aberta">ABERTA</h3>
    <h3 v-else-if="horas >= 17 && horas < 18" id="proxima-fechar">PRÓXIMA DE FECHAR</h3>
    <h3 v-else id="fechada">FECHADA</h3>
    <p>{{ segundos }} segundos já se passaram desde de quando você carregou esta pågina.</p>
    <button
      type="button"
      class="btn btn-primary btn-lg"
      @click="mostrarCarrinho()"
    >Carrinho: {{quantidadeNoCarrinho}} filmes</button>
    <b-row v-if="mostrarFilmes">
      <Filmes :filmes="filmes" :carrinho="carrinho" :items="items"/>
    </b-row>
    <b-row v-else>
      <Carrinho :items="items"/>
    </b-row>
  </b-container>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "bootstrap-vue/dist/bootstrap-vue.css";
import 'bootstrap-vue/dist/bootstrap-vue-icons.min.css';


import Filmes from './components/Filmes.vue'
import Carrinho from './components/Carrinho.vue'


export default {
  name: "App",
  components: {Filmes, Carrinho},
  data() {
    return {
      mostrarFilmes: true,
      title: "Locadora de Filmes", //tipo um dicionário, chave e variável
      horas: new Date().getHours(),
      segundos: 0,
      filmes: [
        {
          id: 0,
          titulo: "Star Wars I",
          valor: 10,
          imagem:
            "https://upload.wikimedia.org/wikipedia/commons/6/6c/Star_Wars_Logo.svg",
          descricao:
            "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
          estoqueDisponivel: 3,
          avaliacao: 5
        },
        {
          id: 1,
          titulo: "Star Wars II",
          valor: 20,
          imagem:
            "https://upload.wikimedia.org/wikipedia/commons/6/6c/Star_Wars_Logo.svg",
          descricao:
            "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
          estoqueDisponivel: 7,
          avaliacao: 5
        },
        {
          id: 2,
          titulo: "Star Wars III",
          valor: 30,
          imagem:
            "https://upload.wikimedia.org/wikipedia/commons/6/6c/Star_Wars_Logo.svg",
          descricao:
            "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
          estoqueDisponivel: 5,
          avaliacao: 5
        },
        {
          id: 3,
          titulo: "Star Wars IV",
          valor: 30,
          imagem:
            "https://upload.wikimedia.org/wikipedia/commons/6/6c/Star_Wars_Logo.svg",
          descricao:
            "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
          estoqueDisponivel: 2,
          avaliacao: 5
        },
        {
          id: 4,
          titulo: "Star Wars V",
          valor: 20,
          imagem:
            "https://upload.wikimedia.org/wikipedia/commons/6/6c/Star_Wars_Logo.svg",
          descricao:
            "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
          estoqueDisponivel: 8,
          avaliacao: 5
        },
        {
          id: 5,
          titulo: "Star Wars VI",
          valor: 30,
          imagem:
            "https://upload.wikimedia.org/wikipedia/commons/6/6c/Star_Wars_Logo.svg",
          descricao:
            "<b>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</b>",
          estoqueDisponivel: 9,
          avaliacao: 3
        },
      ],
      items: {},
      carrinho: [],
    };
  },
  methods: {
    slug(texto) {
      return texto
        .toLowerCase()
        .replace(/[^\w ]+/g, "")
        .replace(/ +/g, "-");
    },
    mostrarCarrinho() {
      this.mostrarFilmes = this.mostrarFilmes ? false : true;
    }
  },
  created() {
    setInterval(() => {
      this.segundos++;
    }, 1000);
    
    this.items.quantidade = [];
    this.items.valor = [];
    for (let i = 0; i < this.filmes.length; i++) {
      this.items.quantidade.push(0);
    }
    for (let i = 0; i < this.filmes.length; i++) {
      this.items.valor.push(0);
    }
  },
  computed: {
    quantidadeNoCarrinho() {
      return this.carrinho.length;
    },
  },
};
</script>

<style>
#aberta {
  color: blue;
}
#proxima-fechar {
  color: orange;
}
#fechada {
  color: red;
}
.container {
  text-align: center;
}
.invisible {
  display: none;
}
</style>
