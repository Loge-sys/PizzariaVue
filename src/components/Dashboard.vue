<template>
  <div id="pizza-table">
    <Message :msg="msg" v-show="msg"/>
    <div>
      <div id="pizza-table-head">
        <div class="order-id">Id</div>
        <div>Cliente:</div>
        <div>Tamanho:</div>
        <div>Sabor:</div>
        <div>Opcionais</div>
        <div>Opr.</div>
      </div>
    </div>
    <div id="pizza-table-rows">
      <div class="pizza-table-row" v-for="pizza in pizzas" :key="pizza.id">
        <div class="order-number">{{pizza.id}}</div>
        <div>{{pizza.nome}}</div>
        <div>{{pizza.tamanho}}</div>
        <div>{{pizza.sabor}}</div>
        <div>
          <ul>
            <li v-for="(opcional, index) in pizza.opcionais" :key="index">{{opcional}}</li>
          </ul>
        </div>
        <div>
          <select name="status" class="status" @change="updatedPizza($event, pizza.id)">
            <option value="">Selecione</option>
            <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="pizza.status === s.tipo">
                {{s.tipo}}
            </option>
          </select>
          <button class="delete-btn" @click="deletePizza(pizza.id)">Cancelar</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Message from './Message.vue'
export default {
  name: "Dashboard",
  data(){
    return {
        pizzas: null,
        pizza_id: null,
        status: [],
        msg: null
    }
  },
  components: {
    Message
  },
  methods: {
    async getPedidos(){
        const req = await fetch('http://localhost:3000/pizzas')

        const data = await req.json()

        this.pizzas = data

        this.getStatus()

    },
    async getStatus(){
        const req = await fetch('http://localhost:3000/status')

        const data = await req.json()

        this.status = data
    },
    async deletePizza(id){
        const req = await fetch(`http://localhost:3000/pizzas/${id}`, {
            method: "DELETE"
        })

        const res = await req.json()
        this.msg = "Pedido cancelado com sucesso"

        setTimeout(() => this.msg = "", 3000)
        this.getPedidos()

    },
    async updatedPizza(event, id){
        const option = event.target.value
        
        const dataJson = JSON.stringify({status: option})

        const req = await fetch(`http://localhost:3000/pizzas/${id}`, {
            method: 'PATCH',
            headers: { "Content-Type" : "application/json" },
            body: dataJson
        })
        const res = await req.json()
        this.msg = `Pedido N°${res.id} foi atualizado para ${res.status}!`

        setTimeout(() => this.msg = "", 3000)
    }
  },
  mounted(){
    this.getPedidos()
  }
};
</script>

<style scoped>
#pizza-table {
  max-width: 1200px;
  margin: 0 auto;
}

#pizza-table-head,
#pizza-table-rows,
.pizza-table-row {
  display: flex;
  flex-wrap: wrap;
}

#pizza-table-head {
  font-weight: bold;
  padding: 12px;
  border-bottom: 3px solid #333;
}
#pizza-table-head div,
.pizza-table-row div {
  width: 19%;
}
.pizza-table-row {
  width: 100%;
  padding: 12px;
  border-bottom: 1px solid #ccc;
}
#pizza-table-head .order-id,
.pizza-table-row .order-number {
  width: 5%;
}

select {
  padding: 12px 6px;
  margin-right: 12px;
}
.delete-btn {
  background-color: #000;
  color: #fff;
  font-weight: bold;
  border: 2px solid #222;
  padding: 10px;
  margin: 0 auto;
  cursor: pointer;
  transition: 0.5s;
}
.delete-btn:hover {
  background-color: #f5f7c2;
  color: #000;
}
</style>