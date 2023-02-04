<template>
    <form>
      <p>¿Qué quieres hacer?</p>
      <div>
        <input type="checkbox" value="500" v-model="price" @change="enabled = !this.enabled"><label>Una página web (500€)</label>
        <PanelItem @numberPages="pages = $event" @numberLanguages="languages = $event" :isEnabled="this.enabled"></PanelItem>
      </div>
      <div>
        <input type="checkbox" value="300" v-model="price"><label>Una consultoria SEO (300€)</label>
      </div>
      <div>
        <input type="checkbox" value="200" v-model="price"><label>Una campaña de Google Ads (200€)</label>
      </div>

      <p>Precio: {{ total }} €</p>

      <div>
        <label class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Nombre Presupuesto:</label>
        <input type="text" v-model="name" class="block mx-auto p-2 text-gray-900 border border-gray-300 rounded-lg bg-gray-50 sm:text-xs focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
      </div>
      <div>
        <label class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Cliente</label>
        <input type="text" v-model="client" class="block mx-auto p-2 text-gray-900 border border-gray-300 rounded-lg bg-gray-50 sm:text-xs focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
      </div>

      <button @click.prevent="mountList()" class="bg-transparent hover:bg-blue-500 text-blue-700 font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded">Enviar</button>

      <ListItem :pressupostList="this.pressupostList" class="absolute inset-y-10 right-20 w-42 mt-0"></ListItem>
    </form>
</template>

<script>
import PanelItem from './Panel.vue'
import ListItem from './List.vue'

export default {
  name: 'HomeForm',
  components: {
    PanelItem, ListItem
  },
  data() {
    return {
      price: [],
      total: 0,
      pages: 1,
      languages: 1,
      enabled: false,
      name: '',
      client: '',
      pressupostList: []
    }
  },
  watch: {
    price: function() {
      this.calculateTotal();
    },
    pages: function() {
      this.calculateTotal();
    },
    languages: function() {
      this.calculateTotal();
    },
    enabled: function() {
      this.calculateTotal();
    },
  },
  methods: {
    calculateTotal() {
      let sum = this.price.map(e => +e).reduce((a, b) => a + b, 0);
      let panelSum = (this.pages * this.languages * 30) * this.enabled;
      let totalSum = sum + panelSum
      let result = this.total = totalSum;
      return result;      
    },
    mountList() {
      const pressupost = {
        name: this.name,
        client: this.client,
        services: [],
        pages: this.pages,
        languages: this.languages,
        total: this.total 
      }
      if (this.name && this.client != '' && this.total != 0) {
        this.pressupostList.push(pressupost);
      }

      if (this.enabled == false) {
        pressupost.pages = 0;
        pressupost.languages = 0;
      }

      if (this.price.includes('500')) {
        pressupost.services.push("Página web");
      } 
      
      if (this.price.includes('300')) {
        pressupost.services.push("Consultoria SEO");
      } 
      
      if (this.price.includes('200')) {
        pressupost.services.push("Campaña Google ADs");
      }
    }
  }
}
</script>

<style scoped>
  div {
    margin-top: 12px;
    margin-bottom: 12px;
  }
</style>
