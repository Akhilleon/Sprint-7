<template>
    <form>
      <p>¿Qué quieres hacer?</p>
      <div>
        <input type="checkbox" value="500" v-model="price" @change="enabled = !this.enabled;"><label>Una página web (500€)</label>
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
import PanelItem from '@/components/Panel.vue'

export default {
  name: 'HomeForm',
  components: {
    PanelItem
  },
}
</script>