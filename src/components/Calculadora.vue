<script setup>
import { reactive } from 'vue';

const estado = reactive({
    primeiroNumero: '',
    segundoNumero: '',
    operacoes: {
        soma: (a, b) => a + b,
        subtracao: (a, b) => a - b,
        multiplicacao: (a, b) => a * b,
        divisao: (a, b) => (b !== 0 ? a / b : 'Divisão por zero'),  
        // Divide a por b, mas se b for igual a 0, retorna a string 'Divisão por zero' para evitar um erro.

    },
    resultado: 0,
});

const calcularResultado = () => {
    const { primeiroNumero, segundoNumero, operacaoMatematica } = estado;
    estado.resultado = estado.operacoes[operacaoMatematica](parseFloat(primeiroNumero), parseFloat(segundoNumero));
}; 
//estado.operacoes[operacaoMatematica]: Seleciona a função de operação matemática correspondente
// parseFloat(primeiroNumero) e parseFloat(segundoNumero): Converte os valores de primeiroNumero e segundoNumero de strings
// para números de ponto flutuante, pois as operações matemáticas requerem números.

</script>



<template>
    <div class="container  p-4 mt-4 rounded shadow-sm">
        <h1 class="text-center mb-4">Calculadora Aritmética VueJs</h1>

        <div class="mb-3">
            <input type="text" class="form-control" v-model="estado.primeiroNumero" @input="calcularResultado" placeholder="Primeiro número"/>
        </div>
        <!-- v-model="estado.primeiroNumero": Liga o valor do input ao estado reativo. Sempre que o usuario digitar o 1 numero, o valor sera atualizado -->
        <!-- @input="calcularResultado": Este evento é acionado toda vez que o valor do input é alterado. O método calcularResultado é chamado, que atualiza o resultado da operação aritmética. -->
        <div class="mb-3">
            <input type="text" class="form-control" v-model="estado.segundoNumero" @input="calcularResultado" placeholder="Segundo número"/>
        </div>

        <div class="mb-3">
            <select class="form-select" v-model="estado.operacaoMatematica" @change="calcularResultado">
                <option value="soma">Soma</option>
                <option value="subtracao">Subtração</option>
                <option value="multiplicacao">Multiplicação</option>
                <option value="divisao">Divisão</option>
            </select>
        </div>

        <p class="text-center result">Resultado: {{ estado.resultado }}</p>
    </div>
</template>

<style scoped>
.container {
    max-width: 340px;
    margin: 0 auto;
    background-color: rgb(228, 185, 205);
}

.result {
    font-weight: bold;
    font-size: 1.2em;
    margin-top: 10px;
}
</style>
