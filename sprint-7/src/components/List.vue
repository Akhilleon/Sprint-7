<template>
    <div>
        <div>
            <label>Buscar: </label><input type="text" v-model="search" class="inline mx-auto my-2 p-2 text-gray-900 border border-gray-300 rounded-lg
             bg-gray-50 sm:text-xs focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
        </div>
        <button @click.prevent="sortArray('alfabeticamente')" class="bg-blue-500 text-white active:bg-blue-600 font-bold uppercase text-xs px-4 py-2 rounded-full 
        shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
            Ordenar alfabéticamente
        </button>
        <button @click.prevent="sortArray('importe')" class="bg-blue-500 text-white active:bg-blue-600 font-bold uppercase text-xs px-4 py-2 rounded-full 
        shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
            Ordenar por importe
        </button>
        <button @click.prevent="sortArray('reiniciar')" class="bg-blue-500 text-white active:bg-blue-600 font-bold uppercase text-xs px-4 py-2 rounded-full 
        shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button">
            Reiniciar
        </button>

        <ul v-if="duplicateList.length">
            <li  v-for="(item, index) in filteredSearch" :key="index">
                {{ `Nombre del presupuesto: ${item.name}` }} <br>
                {{ `Nombre del cliente: ${item.client}` }} <br>
                {{ `Servicios: ${item.services}` }} <br>
                {{ `Paginas: ${item.pages}` }} <br>
                {{ `Idiomas: ${item.languages}` }} <br>
                {{ `Total: ${item.total} €` }} 
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: 'ListItem',
        data () {
            return {                
                duplicateList: [],
                search: ''
            }
        },
        props: ['pressupostList'],
        methods: {
            sortArray(orden) {
                if (orden == 'alfabeticamente') {
                    this.duplicateList = this.duplicateList.sort((a, b) => (a.name > b.name ? 1 : -1));
                }
                if (orden == 'importe') {
                    this.duplicateList = this.duplicateList.sort((a, b) =>  a.total - b.total);
                }
                if (orden == 'reiniciar') {
                    this.duplicateList = [...this.pressupostList];
                }
            }
        },
        watch: {
            pressupostList: {
                handler(newValue) {
                this.duplicateList = [...newValue];  
        },
            deep: true
        }
    },
        computed: {
            filteredSearch() {
                return this.duplicateList.filter(pressupost => {
                    return pressupost.name.toLowerCase().includes(this.search.toLowerCase());
                });
            }
        }
}
</script>