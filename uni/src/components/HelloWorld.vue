<template lang="pug">
  v-container.justify-center.form-career(fluid)
    v-form.mt-5
      h1 Nueva Carrera
      v-layout.mt-5
        v-flex.xs-12
          label Nombre
          input.input-career(placeholder="Nombre", v-model='name')
      v-layout.mt-3
        v-flex.xs-6
          label Código
          input.input-career(v-model='code')
        v-flex.xs-6
          label Facultad
          select(v-model='facultie')
            option Seleccione
            option(v-for='facultie in faculties') {{facultie}}
      h2.mt-3.mb-3.blue--text Cursos por carrera
      v-card.pa-4
        h3 Ciclo 1
        v-autocomplete(v-model='courses', :disabled='isUpdating', :items='optionCourses', chips='', color='', box='', placeholder='Agregar curso a ciclo' item-text='name', item-value='name', multiple='')
          template(v-slot:selection='data')
            v-chip.chip--select-multi(:selected='data.selected', color='primary', text-color='white' close='', @input='remove(data.item)')
              |{{ data.item.name }}
          template(v-slot:item='data')
            template(v-if="typeof data.item !== 'object'")
              v-list-tile-content(v-text='data.item')
            template(v-else='')
              v-list-tile-content
                v-list-tile-title(v-html='data.item.name')
      template
      .text-xs-center
        v-dialog(width='500')
          template(v-slot:activator='{ on }')
            v-btn(color='red lighten-2', dark='', v-on='on')
              | Click Me
          v-card
            v-card-title.headline.grey.lighten-2(primary-title='')
              | Datos
            v-card-text
              p Nombre: {{name}}
              p Código: {{code}}
              p Facultad: {{facultie}}
              ol 
                li(v-for='course in courses') {{course}}
              
</template>

<script>

export default {
    data () {
      return {
        autoUpdate: true,
        courses: [
          { name: 'Sandra Adams', group: 'Group 1' },
          { name: 'Ali Connors', group: 'Group 1'},
        ],
        isUpdating: false,
        name: '',
        code: '',
        facultie: '',
        optionCourses: [
          { header: 'Group 1' },
          { name: 'Sandra Adams', group: 'Group 1' },
          { name: 'Ali Connors', group: 'Group 1'},
          { name: 'Trevor Hansen', group: 'Group 1' },
          { name: 'Tucker Smith', group: 'Group 1'},
        ],
        faculties: ['Matemática', 'Educación'],

      }
    },

    methods: {
      remove (item) {
        const index = this.courses.name.indexOf(item.name)
        if (index >= 0) this.courses.splice(index, 1)
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="sass">
.form-career
  .v-form
    width: 70%;
    margin: 0 auto;

  label
    margin-right: 14px;
    width: 3.5em;
    display: inline-block;

  .input-career, select
    border: 1px solid gray;
    border-radius: 4px;
    width: 25em;
    padding: .375rem .75rem;
    font-size: 1rem;
    line-height: 1.5;
    color: #495057;
    background-color: #fff;
    background-clip: padding-box;
    border: 1px solid #ced4da;
    border-radius: .25rem;
    transition: border-color .15s 

  .v-chip
    height: 2em;
    width: 13em;
    border-radius: 4px;
    position: relative;

  .v-chip__close>.v-icon
    position: absolute;
    right: 7px;
    height: 2em;
    background-color: transparent;

  .theme--light.v-text-field--box>.v-input__control>.v-input__slot
    background: white;
    &:hover
      background: none;
  .theme--light.v-icon
    color: white;
  .v-autocomplete:not(.v-input--is-disabled).v-select.v-text-field input 
    border: 1px solid gray;
    border-radius: 4px;
  .v-input input 
    max-height: 27px;
    width: 3em;

  .v-autocomplete__content.v-menu__content, .v-autocomplete__content.v-menu__content .v-card
    min-width: auto !important;
</style>
