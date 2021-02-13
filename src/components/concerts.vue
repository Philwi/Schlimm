<template lang="pug">
.concerts
  v-card(style="background-color: #329676;")
    v-card-title(class="headline" style="color: #fff; margin: auto;") Zukünftige Konzerte
    v-card-text
      v-expansion-panels(accordion focusable='' dark="")
        v-expansion-panel(v-for='konzert in konzerte')
          v-expansion-panel-header
            v-layout(row wrap)
              v-flex(xs12 md4 lg4)
                | {{ konzert.ort }}
              v-flex(xs12 md4 lg4 offset-md4 offset-lg4 style="text-align: right;")
                | {{ date_format(konzert.date) }}
          v-expansion-panel-content
            v-card(style="overflow: auto;")
              v-card-text
                v-layout(row wrap)
                  v-flex(xs12 md4 lg4)
                    b Club:
                  v-flex(xs12 md8 lg8)
                    p {{ konzert.club }}
                v-layout(row wrap)
                  v-flex(xs12 md4 lg4)
                    b Weitere Bands:
                  v-flex(xs12 md8 lg8)
                    p {{ konzert.bands }}
                template(v-if='(konzert.description != "")')
                  v-layout(row wrap)
                    v-flex(xs12 md4 lg4)
                      b Beschreibung:
                    v-flex(xs12 md8 lg8)
                      p {{ konzert.description }}
                template(v-if='(konzert.veranstaltungslink != "")')
                  v-layout(row wrap)
                    v-flex(xs12 md4 lg4)
                      b Veranstaltung:
                    v-flex(xs12 md8 lg8)
                      a(style="color: lightgrey;") {{ konzert.veranstaltungslink }}
</template>

<script>
export default {
  data: function (){
    return {
      name: 'konzerte',
      dialog: false,
      konzerte: [
        {
          ort: 'No shows planned',
          date: 'tba',
          club: 'Unbekannt',
          bands: 'Unbekannt',
          description: 'Through corona there are no shows planned yet :(',
          veranstaltungslink: ''
        }
      ]
    }
  },
  methods: {
    date_format(date){
      var d = new Date(date);
      return d.toLocaleDateString("de");
    },
  },
  created(){
  },
  watch: {
  }
}
</script>

<style lang="sass">

</style>
