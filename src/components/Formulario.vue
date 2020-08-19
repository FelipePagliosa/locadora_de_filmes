<template>
     <b-col>
        <b-form class="textleft">
          <b-row class="form-row">
            <b-form-group
              id="input-group-1"
              label="Primeiro nome:"
              label-for="input-1"
              class="col-6"
            >
              <b-form-input
                id="input-1"
                v-model.lazy="pedido.primeiroNome"
                type="text"
                required
                placeholder="Nome"
              ></b-form-input>
            </b-form-group>

            <b-form-group
              id="input-group-2"
              label="Seu sobrenome:"
              label-for="input-2"
              class="col-6"
            >
              <b-form-input
                id="input-2"
                v-model.trim.lazy="pedido.ultimoNome"
                required
                placeholder="Sobrenome"
              ></b-form-input>
            </b-form-group>
          </b-row>

          <b-form-group id="input-group-3" label="Endereço:" label-for="input-3">
            <b-form-input
              id="input-3"
              v-model.trim.lazy="pedido.endereco"
              required
              placeholder="Endereço"
            ></b-form-input>
          </b-form-group>

          <b-row>
            <b-form-group id="input-group-4" label="Cidade:" label-for="input-4" class="col-4">
              <b-form-input
                id="input-4"
                v-model.trim.lazy="pedido.cidade"
                required
                placeholder="Cidade"
              ></b-form-input>
            </b-form-group>

            <b-form-group id="input-group-5" label="Estado:" label-for="estado" class="col-4">
              <select class="form-control" id="estado" v-model="pedido.estado">
                <option disabled value>Escolha um estado</option>
                <!-- como é um objeto, e não uma lista de objetos, tem que usar a palavra reservada key, pq é chave: valor, se fosse array usaria index -->
                <option
                  v-for="(estado, key) in estados"
                  v-bind:value="estado"
                  v-bind:key="key"
                >{{ key }}</option>
              </select>
            </b-form-group>

            <b-form-group id="input-group-5" label="CEP" label-for="input-5" class="col-4">
              <b-form-input
                id="input-5"
                v-model.number.lazy="pedido.cep"
                required
                placeholder="CEP"
              ></b-form-input>
            </b-form-group>
          </b-row>

          <div class="form-group form-check">
            <input
              type="checkbox"
              class="form-check-input"
              id="pagoNaEntrega"
              v-bind:true-value="pedido.simNaEntrega"
              v-bind:false-value="pedido.naoNaEntrega"
              v-model="pedido.pagoNaEntrega"
            />
            <label class="form-check-label" for="pagoNaEntrega">Pago na entrega?</label>
          </div>
          <div class="form-group form-check-inline">
            <input
              type="radio"
              class="form-check-input"
              id="manha"
              value="Manhã"
              v-model="pedido.entrega"
            />
            <label class="form-check-label" for="manha">Manhã</label>
          </div>
          <div class="form-group form-check-inline">
            <input
              type="radio"
              class="form-check-input"
              id="tarde"
              value="Tarde"
              v-model="pedido.entrega"
            />
            <label class="form-check-label" for="tarde">Tarde</label>
          </div>
          <div class="form-group form-check-inline">
            <input
              type="radio"
              class="form-check-input"
              id="noite"
              value="Noite"
              v-model="pedido.entrega"
            />
            <label class="form-check-label" for="noite">Noite</label>
          </div>
          <b-button type="submit" variant="dark" block>Finalizar pedido</b-button>
        </b-form>
        <p>
          Primeiro nome: {{ pedido.primeiroNome }}
          Último nome: {{ pedido.ultimoNome }}
          Endereço: {{ pedido.endereco }}
          Cidade: {{ pedido.cidade }}
          Estado: {{ pedido.estado }}
          Cep: {{pedido.cep}}
          Pago na entrega?: {{ pedido.pagoNaEntrega }}
          Entrega: {{ pedido.entrega }}
        </p>
    </b-col>
</template>

<script>
export default {
    name:'Formulario',
    components: {},
    data(){
        return{
            estados: { RJ: "Rio de Janeiro",MG: "Minas Gerais",SP: "São Paulo",ES: "Espírito Santo",},
            pedido: {primeiroNome: "",ultimoNome: "",endereco: "",cidade: "",estado: "",cep: "",pagoNaEntrega: "Não",simNaEntrega: "Sim",naoNaEntrega: "Não",entrega: "Manhã"},
        }
    }
}
</script>

<style  scoped>
    .textleft {
        text-align: left;
    }
</style>