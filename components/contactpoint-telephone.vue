<template>
  <v-container>
    <v-row>
      <v-col cols="12">
        <pre>{{parse(telephone)}}</pre>
      </v-col>
      <v-col :cols="ui?.show?.includes('whatsapp') ? 6 : 12">
        <v-btn prepend-icon="mdi-phone" :href="`tel:${telephone}`" title="Ligar para telefone" block>
          Ligar
        </v-btn>
      </v-col>
      <v-col 
        v-if="ui?.show?.includes('whatsapp')"
        :cols="6"
      >
        <v-btn 
          prepend-icon="mdi-phone" 
          :href="`https://wa.me/${telephone}?text=${message}`"
          target="_blank" 
          title="Envia mensagem no WhatsApp" 
          block
        >
          WhastApp
        </v-btn>
      </v-col>
      <!-- <v-col cols="6">
        <v-btn prepend-icon="mdi-copy" title="Copiar Telefone" block>
          Copiar
        </v-btn>
      </v-col> -->
    </v-row>
  </v-container>
</template>
<script>
export default {
  props: {
    telephone: String,
    message: String,
    ui: {
      type: Object,
      default: {},
    }
  },
  methods: {
    parse(str) {
      const number = str.slice(5)
      let numberParsed = null
      if (number.length > 8) {
        numberParsed = number.match(/.{1,5}/g).join('-')
      } else {
        numberParsed = number.match(/.{1,4}/g).join('-')
      }
      return `${str.slice(0,3)} ${str.slice(3,5)} ${numberParsed}`
    }
  },
}
</script>
