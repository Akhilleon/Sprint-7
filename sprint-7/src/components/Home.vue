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

      <p>Precio: {{ total }}€</p>
    </form>
</template>

<script>
import PanelItem from './Panel.vue'

export default {
  name: 'HomeForm',
  components: {
    PanelItem
  },
  data() {
    return {
      price: [],
      total: 0,
      pages: 1,
      languages: 1,
      enabled: false
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
    }
  },
  methods: {
    calculateTotal() {
      let sum = this.price.map(e => +e).reduce((a, b) => a + b, 0);
      let panelSum = (this.pages * this.languages * 30) * this.enabled;
      let totalSum = sum + panelSum
      let result = this.total = totalSum;
      return result;      
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
