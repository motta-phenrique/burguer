<template>
<div class="container">

    <Message :msg="msg" v-show="msg" />

    <form @submit="createBurguer">
        <div class="input-container">
            <label for="nome">Nome: </label>
            <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite seu nome">
        </div>
        <div class="input-container">
            <label for="pao">Escolha o Pão:</label>
            <select name="pao" id="pao" v-model="pao">
                <option value="">Selecine seu pão:</option>
                <option v-for="pao in paes" :value="pao.tipo" :key="pao.id">{{ pao.tipo }}</option>
            </select>
        </div>

        <div class="input-container">
            <label for="carne">Escolha a carne:</label>
            <select name="carne" id="carne" v-model="carne">
                <option value="">Selecine sua carne:</option>
                <option v-for="carne in carnes" :value="carne.tipo" :key="carne.id">{{ carne.tipo }}</option>
            </select>
        </div>

        <div class="input-container">
            <label for="opcionais">Selecione os opcionais:</label>
            <div class="checkbox-container" v-for="op in opcionaisdata" :key="op.id">
                <input type="checkbox" name="opcionais" v-model="opcionais" :value="op.tipo">
                <span>{{ op.tipo }}</span>
            </div>
        </div> 

        <div class="input-container">
            <input type="submit" class="submit-btn" value="Criar meu Burguer">
        </div>
    </form>
</div>

</template>

<script>
import Message from './Message.vue';

export default{
     name: "Formulario",
     data() {
        return{
            paes: '',
            carnes: '',
            opcionaisdata: '',
            nome: '',
            pao: '',
            opcionais: [],
            status: 'Solicitado',
            msg: ''
        }
     },
     components:{
        Message
     },
     methods:{
        async getIngredientes(){
            const req = await fetch("http://localhost:3000/ingredientes");
            const data = await req.json();
         

            this.paes = data.paes;
            this.carnes = data.carnes;
            this.opcionaisdata = data.opcionais;
        },

        async createBurguer(e){
            e.preventDefault();
            const data = {
                nome: this.nome,
                carne:this.carne,
                pao:this.pao,
                opcionais: Array.from(this.opcionais),
                status: 'Solicitado'
            }

            const dataJson = JSON.stringify(data);

            const req = await fetch("http://localhost:3000/burgers", {
                method: "POST",
                headers: {"Content-type":"application/json"},
                body: dataJson
            })

            const res = await req.json()

            this.msg = `Pedido Nº${res.id} realizado com sucesso`

            setTimeout(()=> this.msg = "", 3000)

            this.nome = ""
            this.carne = ""
            this.pao = ""
            this.opcionais = []
        }
     },
     mounted(){
        this.getIngredientes()
     }
}

</script>

<style scoped>

  .container{
      display: flex;
      justify-content: center;
      flex-direction:column ;
  }

  #burger-form {
    max-width: 400px;
    margin: 0 auto;
  }

  .input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
  }

  label {
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;;
    padding: 5px 10px;
    border-left: 4px solid #fcba03;
  }

  input, select {
    padding: 5px 10px;
    width: 300px;
  }

  #opcionais-container {
    flex-direction: row;
    flex-wrap: wrap;
  }

  #opcionais-title {
    width: 100%;
  }

  .checkbox-container {
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px;
    padding: 4px;
  }

  .checkbox-container span,
  .checkbox-container input {
    width: auto;
  }

  .checkbox-container input {
    margin-left: 10px;
  }

  .checkbox-container span {
    margin-left: 6px;
    font-weight: bold;
  }

  .submit-btn {
    background-color: #222;
    color:#fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }

  .submit-btn:hover {
    background-color: transparent;
    color: #222;
  }
</style>