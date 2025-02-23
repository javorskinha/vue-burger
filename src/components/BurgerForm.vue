<template>
    <div>
        <p>componente mensagem</p>
        <div>
            <form id="burger-form">
                <div class="input-container">
                    <label for="nome">Nome do cliente:</label>
                    <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite seu nome">
                </div>
                <div class="input-container">
                    <label for="pao">Escolha o pão:</label>
                    <select name="pao" id="pao" v-model="pao">
                        <option value="">Selecione</option>
                        <option value="integral">Integral</option>
                    </select>
                </div>
                <div class="input-container" id="opcionais-container">
                    <label for="carne">Escolha sua proteiína:</label>
                    <select name="carne" id="carne" v-model="carne">
                        <option value="">Selecione</option>
                        <option value="maminha">maminha</option>
                    </select>
                </div>
                <div class="input-container">
                    <label for="opcionais"a id="opcionais-title">Selecione os opcionais:</label>
                    <div id="checkbox-container">
                        <input type="checkbox" name="opcionais" id="opcionais" v-model="opcionais" value="salame">
                        <span class="span">Salame</span>
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
    export default{
        name: 'BurgerForm'
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




