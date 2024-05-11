<script setup>
import { reactive } from 'vue';

const estado = reactive({
    firstNumber: '',
    secondNumber: '',
    result: 0,
    operation: {
        adicao: (a, b) => a + b,
        subtracao: (a, b) => a - b,
        divisao: (a, b) => (b !== 0 ? a / b : 'Erro: não é possível dividir por 0'),
        multiplicacao: (a, b) => a * b
    },
    symbol: ''
})

function calculator() {
    const { firstNumber, secondNumber, mathOperations } = estado
    estado.result = estado.operation[mathOperations](parseFloat(firstNumber), parseFloat(secondNumber))
}

function changeSymbol() {
    switch (estado.mathOperations) {
        case "adicao":
            return estado.symbol = "+"
            break
        case "subtracao":
            return estado.symbol = "-";
            break
        case "divisao":
            return estado.symbol = "/";
            break
        case "multiplicacao":
            return estado.symbol = "x";
            break
        default:
            return ""
    }
}
</script>

<template>
    <form @submit.prevent class="bg-light p-4 rounded-3">
        <div class="row mt-4 justify-content-between align-items-center">
            <div class="col-5">
                <input class="text-center w-100 rounded-2 bg-dark border-0" required type="number"
                    v-model="estado.firstNumber" @input="calculator()">
            </div>
            <div class="col-2 p-0 text-center">
                <button class="badge rounded-2 bg-dark border-1 w-50">{{ estado.symbol }}</button>
            </div>
            <div class="col-5">
                <input class="text-center w-100 rounded-2 bg-dark border-0" required type="number"
                    v-model="estado.secondNumber" @input="calculator()">
            </div>
        </div>
        <div class="row mt-2 align-items-center justify-content-around">
            <div class="col-7 text-center p-0">
                <label class="lead">Selecione a operação:</label>
            </div>
            <div class="col-5">
                <select class="text-center w-100 rounded-2 bg-dark border-1" v-model="estado.mathOperations"
                    @change="calculator(), changeSymbol()">
                    <option value="adicao">Adição</option>
                    <option value="subtracao">Subtração</option>
                    <option value="divisao">Divisão</option>
                    <option value="multiplicacao">Multiplicação</option>
                </select>
            </div>
        </div>
    </form>
    <div class="row mt-2 bg-light p-4 rounded-3">
        <div class="col">
            <p class="lead">Resultado: {{ estado.result }}</p>
        </div>
    </div>
</template>