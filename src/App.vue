<template>
    <v-content>
      <Coindesk/>
    </v-content>
  </v-app>
</template>

<script>
import Coindesk from './components/Coindesk.vue'

export default {
  name: 'App',
  components: {
    Coindesk
  },
  data () {
    return {
      //
    }
  }
}
</script>
