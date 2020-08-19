<template>
    <b-col>
        <Formulario/>
        <b-table
            responsive
            striped
            hover
            head-variant="dark"
            borderless
            :items="carrinhoSemEspacos"
            style="margin-top: 20px"
        ></b-table>
        <p v-if="valorTotal>0">{{valorTotal}}</p>
    </b-col>
</template>


<script>
import Formulario from './Formulario.vue'
export default {
    name:'Carrinho',
    components:{Formulario},
    props:{
        items:Object
    },
    computed:{
        carrinhoSemEspacos() {
            let carrinhoSemEspacos = [];
            for (let i = 0; i < 6; i++) {
                if (this.items.quantidade[i] > 0) {
                    carrinhoSemEspacos.push({
                        nome: `Star Wars ${i + 1}`,
                        quantidade: this.items.quantidade[i],
                        valor: this.items.valor[i],
                    });

                }
            }
            return carrinhoSemEspacos;
        },
        valorTotal(){
            let valorTotal=0
            for (let i = 0; i < 6; i++) {
                if (this.items.quantidade[i] > 0) {
                    valorTotal=valorTotal+(this.items.quantidade[i] * this.items.valor[i])
                }
            }
            return valorTotal
        }
    }
}
</script>

<style  scoped>

</style>