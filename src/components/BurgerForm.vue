<template>
    <div>
        <Mensagem :msg="msg" v-show="msg"/>
        <div>
            <form id="burger-form" @submit="createBurger">
                <div class="input-container">
                    <label for="nome">Nome do cliente:</label>
                    <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite seu nome">
                </div>
                <div class="input-container">
                    <label for="pao">Escolha o pão:</label>
                    <select name="pao" id="pao" v-model="pao">
                        <option value="">Selecione</option>
                        <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{ pao.tipo }}</option>
                    </select>
                </div>
                <div class="input-container" id="opcionais-container">
                    <label for="carne">Escolha sua proteiína:</label>
                    <select name="carne" id="carne" v-model="carne">
                        <option value="">Selecione</option>
                        <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{ carne.tipo }}</option>
                    </select>
                </div>
                <div class="input-container">
                    <label for="opcionais" id="opcionais-title">Selecione os opcionais:</label>
                    <div id="checkbox-container" v-for="opcional in opcionaisData" :key="opcional.id">
                        <input type="checkbox" name="opcionais" id="opcionais" v-model="opcionais" :value="opcional.tipo">
                        <span class="span">{{ opcional.tipo }}</span>
                    </div>
                </div>
                <div class="input-container">
                    <input type="submit" class="submit-btn" value="Criar meu Burger!">
                </div>
            </form>
        </div>
    </div>
</template>

<script>
import Mensagem from './Mensagem.vue';

    export default{
        name: 'BurgerForm',
        data() {
            return {
                paes: null,
                carnes: null,
                opcionaisData: null,
                nome: null,
                pao: null,
                carne: null,
                opcionais: [],
                msg: null
            }
        },
        methods: {
            async getIngredientes (){
                const req = await fetch('http://localhost:3000/ingredientes');
                const data = await req.json();

                this.paes = data.paes;
                this.carnes = data.carnes;
                this.opcionaisData = data.opcionais;
            },
            async createBurger(e){
                e.preventDefault();
                const data = {
                    nome: this.nome,
                    pao: this.pao,
                    carne: this.carne,
                    opcionais: Array.from(this.opcionais),
                    status: 'Solicitado'

                }

                const dataJson = JSON.stringify(data);

                const req = await fetch('http://localhost:3000/burgers', {
                    method: 'POST',
                    headers: {'Content-Type': 'application/json'},
                    body: dataJson
                });

                const res = await req.json();

                //msg de sistema
                this.msg = `Pedido N ${res.id} realizado com sucesso`;

                //lipar msg
                setTimeout(() => this.msg ='', 2000)

                this.nome = '';
                this.pao = '';
                this.carne = '';
                this.opcionais = ';'
            }
        },
        mounted (){
            this.getIngredientes()
        },
        components: {
            Mensagem
        }
    }
</script>

<style scoped>
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
        color: #222;
        padding: 5px 10px;
        border-left: 4px solid #fcba03;
    }

    input, select {
        padding: 5px 10px;
        width: 400px;
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
    }

    .span {
        margin-left: 6px;
        font-weight: bold;
    }

    .checkbox-container span, input{
        width: auto;
    }

    .submit-btn {
        background-color: #222;
        color: #fcba03;
        font-weight: bold;
        border: 2px solid #222;
        padding: 10px;
        font-size: 16px;
        margin: 0 auto;
        width: 70%;
        cursor: pointer;
        transition: .5s;
    }

    .submit-btn:hover {
        background-color: transparent;
        color: #222;
    }
</style>




