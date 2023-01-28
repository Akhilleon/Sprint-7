<template>
    <div id="counter">
        <div class="choices">
            <label>Number of pages </label>
            <button @click.prevent="counterPages++">+</button>
            <input class="inputBoxes" type="number" min="0" v-model="counterPages">
            <button @click.prevent="counterPages > 1 ? counterPages-- : counterPages = 1">-</button>
        </div>
        <div class="choices">
            <label>Number of languages </label>
            <button @click.prevent="counterLanguages++">+</button>
            <input class="inputBoxes" type="number" min="0" v-model="counterLanguages">
            <button @click.prevent="counterLanguages > 1 ? counterLanguages-- : counterLanguages = 1">-</button>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'CounterPanel',
        data() {
            return {
                counterPages: 1,
                counterLanguages: 1
            }
        },
        props: {
                counterEnabled: Boolean
            },
        watch: {
            counterPages: function() {
                if (this.counterEnabled === true) {    
                    this.$emit('numberPages', this.counterPages);
                    this.$emit('numberLanguages', this.counterLanguages);
                } else {
                    this.$emit('numberPages', 1);
                }
            },
            counterLanguages: function() {
                if (this.counterEnabled === true) { 
                    this.$emit('numberLanguages', this.counterLanguages);
                    this.$emit('numberPages', this.counterPages);
                } else {
                    this.$emit('numberLanguages', 1);
                }
            },
            counterEnabled: function() {
                this.counterPages = 1;
                this.counterLanguages = 1;
            }
        }
    }
</script>

<style scoped>
    .choices {
        padding-top: 14px;
        padding-bottom: 14px;
        margin-top: 15px;
        margin-bottom: 15px;
    }
    .inputBoxes {
        width: 5%;
        border: 0;
        
    }
    input::-webkit-outer-spin-button,
    input::-webkit-inner-spin-button {
        -webkit-appearance: none;
        margin: 0;  
    }
</style>