<template>
    <div>
        <h1>Sypání na várku</h1>
    </div>

    <div>
        <h2>EPM</h2>
        <input type="number" step="0.1" min="0" v-model="volume" :placeholder="'Objem mladiny v litrech'">
        <input type="number" step="0.1" min="0" v-model="density" :placeholder="'Hustota mladiny'">
        <input type="number" step="0.1" min="0" v-model="plato" :placeholder="'Hustota v jednotkách plato'">
        <p>Výsledné EPM: {{ calculateEpm }}</p>
    </div>

    <div>
        <br />
        <h2>Přidat slady:</h2>
        <div v-for="(textBox, index) in textBoxes" :key="index">
            <p>Parametry sladu {{ index + 1 }} </p>
            <input type="number" step="0.1" min="0" v-model="extracts[index]" :placeholder="'Extraktivnost ' + (index + 1)">
            <input type="number" step="0.1" min="0" v-model="ratios[index]" :placeholder="'Podíl ' + (index + 1)">
        </div>
        <div>
            <button id="add-button" @click="addTextBoxes">+</button>
        </div>

        <p v-if="totalMultiplication">Celková extraktivnost sladu: {{ totalMultiplication }}</p>
    </div>

    <h2>Efektivita varny:</h2>
    <input type="number" step="0.1" min="0" v-model="efficiency" :placeholder="'Efektivita varny'">
    <br/>
    <button @click="calculateMc">Vypočítat MC</button>
    <p>Výsledné Mc: </p> <p v-if="mc">  {{ mc }}</p>

    <br/>
    <div>
        <h2>Vysvětlení:</h2>
        <ul>
            <li>Extraktivnost a podíl se udává v hmotnostním zlomku</li>
        </ul>
    </div>
</template>

<script>
import '../calc_styles.css';
export default {
    data() {
        return {
            textBoxes: [{}],
            extracts: [],
            ratios: [],
            volume: null,
            density: null,
            plato: null,
            efficiency: null,
            mc: null
        };
    },
    methods: {
        addTextBoxes() {
            this.textBoxes.push({});
        },
        calculateMc() {
            const epm = this.calculateEpm;

            const total = this.totalMultiplication;
            const efficiency = Number(this.efficiency);
            if (isNaN(epm) || isNaN(total) || isNaN(efficiency) || efficiency === 0) {
                console.log(epm + total + efficiency + efficiency)
                return;
            }
            this.mc = epm / (total * efficiency);

        }
    },
    computed: {
        totalMultiplication() {
            let result = 0;
            for (let i = 0; i < this.extracts.length && i < this.ratios.length; i++) {
                result += this.extracts[i] * this.ratios[i];
            }
            return result;
        },
        calculateEpm() {
            if (this.volume && this.density && this.plato) {
                return (0.9982 * this.volume * this.density * (this.plato/100)).toFixed(2);
            } else {
                return null;
            }
        }
    }
};
</script>

