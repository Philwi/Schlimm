<template lang="pug">
.contact
  v-card(style="background-color: #329676;")
    v-form(ref="form" v-model="valid" lazy-validation)
      v-card-text
        v-container(grid-list-md='')
          v-layout(wrap='')
            v-flex(xs12='' sm12='' md12='')
              v-text-field(label='Von' required='' hint='Deine E-Mail' color="#fff" :rules="emailRule" v-model="email")
            v-flex(xs12='' sm12='' md12='')
              v-text-field(label='Betreff' hint='Warum schreibst du uns?' required='' color="#fff" :rules="inputRules" v-model="subject")
            v-flex(xs12='' sm12='' md12='')
              v-textarea(label='Deine Nachricht' required='' hint='Inhalt deiner Nachricht' color="#fff" :rules="inputRules" v-model="body")
      v-card-actions
        .center
          v-btn(color='grey lighten-5' text='' @click.prevent="deliverMessage" :loading="loading" :disable="loading") Abschicken
</template>

<script>
export default {
  data: function (){
    return {
      name: 'nachrichten',
      email: '',
      subject: '',
      body: '',
      valid: true,
      inputRules: [
        v => !!v || 'muss ausgefüllt werden',
        v => (v && v.length >= 4) || 'Mindestens 4 Buchstaben'
      ],
      emailRule: [
        v => !!v || 'E-mail muss ausgefüllt werden',
        v => /.+@.+/.test(v) || 'Muss eine gültige E-Mail sein'
      ],
      loader: null,
      loading: false
    }
  },
  created(){
    this.dialog= true;
  },
  watch: {
    loader(){
      const l = this.loader
      this[l] = !this[l]
      setTimeout(function(){
      }.bind(this), 20000)
      this.loader = null
    }
  },
  methods: {
    deliverMessage(){
      if (this.$refs.form.validate()){
        console.log(true)
      }
    }
  }
}
</script>

<style lang="sass">
.v-text-field
  color: #fff !important
.theme--light.v-input:not(.v-input--is-disabled) input, .theme--light.v-input:not(.v-input--is-disabled) textarea
  color: #fff !important

.center
  margin: auto

</style>

