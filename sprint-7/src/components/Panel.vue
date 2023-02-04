<template>
    <div id="panel" v-show="this.isEnabled">
        <CounterPanel @numberPages="addonPages = $event" @numberLanguages="addonLanguages = $event" :counterEnabled="this.isEnabled"></CounterPanel>
    </div>
</template>

<script>
import CounterPanel from './Counter.vue'

    export default {
        name: 'PanelItem',
        components: {
            CounterPanel
        },
        data() {
            return {
                addonPages: 1,
                addonLanguages: 1
            }
        },
        props: {
            isEnabled: Boolean
        },
        watch: {
            addonPages: function() {
                if (this.isEnabled === true) {    
                    this.$emit('numberPages', this.addonPages);
                    this.$emit('numberLanguages', this.addonLanguages);
                } else {
                    this.$emit('numberPages', 1);
                }
            },
            addonLanguages: function() {
                if (this.isEnabled === true) { 
                    this.$emit('numberLanguages', this.addonLanguages);
                    this.$emit('numberPages', this.addonPages);
                } else {
                    this.$emit('numberLanguages', 1);
                }
            }
        }
    }
</script>

<style scoped>
    #panel {
        margin: 15px auto 15px auto;
        width: 420px;
        border: solid 3px;
        border-radius: 20px;
    }
</style>