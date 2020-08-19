<template>
    <div class="cards">
        <b-card
          :title="filme.titulo"
          :img-src="filme.imagem"
          :img-alt="filme.descricao"
          img-top
          tag="article"
          style="max-width: 20rem;"
          class="mb-2"
          :key="filme.id"
          v-for="filme in filmes"
        >
          <!-- pode ser v-bind e outra propriedade, tipo id e value -->
          <b-card-text>
            <b-icon variant="warning" icon="star-fill" font-scale="1" v-for="n in filme.avaliacao" :key="n+'fill'"></b-icon>
            <b-icon icon="star" font-scale="1" variant="warning" v-for="n in (5 - filme.avaliacao)" :key="n"></b-icon>
          </b-card-text>
          <a
            href="#"
            @click="adicionarAoCarrinho(filme)"
            v-if="(filme.estoqueDisponivel-quantidadeNoCarrinhoPorFilme(filme)<=2) && validarPermissaoParaAdicionarNoCarrinho(filme)"
            class="btn btn-primary"
          >Apenas {{ filme.estoqueDisponivel - quantidadeNoCarrinhoPorFilme(filme)}} restantes</a>
          <a
            href="#"
            @click="adicionarAoCarrinho(filme)"
            v-else-if="validarPermissaoParaAdicionarNoCarrinho(filme)"
            class="btn btn-primary"
          >Alugar</a>
          <a href="#" v-else class="btn btn-warning disabled">Esgotado</a>
          <b-card-text>{{ filme.descricao }}</b-card-text>
        </b-card>
    </div>
</template>

<script>
export default {
    name:'Filmes',
    props:{
        filmes:Array,
        items:Object,
        carrinho:Array
    },
    methods: {
        quantidadeNoCarrinhoPorFilme(filme) {
            let quantidade = 0;
            for (let i = 0; i < this.carrinho.length; i++) {
                if (filme.id == this.carrinho[i].id) {
                quantidade++;
                }
            }
            return quantidade;
        },
        validarPermissaoParaAdicionarNoCarrinho(filme) {
            return filme.estoqueDisponivel > this.quantidadeNoCarrinhoPorFilme(filme); //retornando resultado dum if
        },
        adicionarAoCarrinho(filme) {
            this.carrinho.push(filme);
            this.items.quantidade[filme.id] += 1;
            this.items.valor[filme.id] += filme.valor;
            console.log(this.items);
        },
    }
}
</script>

<style  scoped>
.cards {
  display: flex;
  align-items: center;
  justify-content: space-around;
  flex-wrap: wrap;
}
.card:hover {
  transform: scale(1.05);
}
</style>