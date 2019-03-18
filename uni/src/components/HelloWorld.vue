<template lang="pug">
  v-container.justify-center.form-career(fluid)
    v-form.mt-5
      h1 Nueva Carrera
      v-layout.mt-5
        v-flex.xs-12
          label Nombre
          input.input-career(placeholder="Nombre")
      v-layout.mt-3
        v-flex.xs-6
          label Código
          input.input-career
        v-flex.xs-6
          label Facultad
          select
            option Seleccione
      h2.mt-3.mb-3.blue--text Cursos por carrera
      v-card.pa-4
        h3 Ciclo 1
        v-autocomplete(v-model='friends', :disabled='isUpdating', :items='people', chips='', color='', box='', placeholder='Agregar curso a ciclo' item-text='name', item-value='name', multiple='')
          template(v-slot:selection='data')
            v-chip.chip--select-multi(:selected='data.selected', color='primary', text-color='white' close='', @input='remove(data.item)')
              |{{ data.item.name }}
          template(v-slot:item='data')
            template(v-if="typeof data.item !== 'object'")
              v-list-tile-content(v-text='data.item')
            template(v-else='')
              v-list-tile-content
                v-list-tile-title(v-html='data.item.name')
        input.input-add.mt-2(placeholder="Agregar curso a ciclo")
          
</template>

<script>

export default {
    data () {
      const srcs = {
        1: 'https://cdn.vuetifyjs.com/images/lists/1.jpg',
        2: 'https://cdn.vuetifyjs.com/images/lists/2.jpg',
        3: 'https://cdn.vuetifyjs.com/images/lists/3.jpg',
        4: 'https://cdn.vuetifyjs.com/images/lists/4.jpg',
        5: 'https://cdn.vuetifyjs.com/images/lists/5.jpg'
      }

      return {
        autoUpdate: true,
        friends: ['Sandra Adams', 'Britta Holt'],
        isUpdating: false,
        name: 'Midnight Crew',
        people: [
          { header: 'Group 1' },
          { name: 'Sandra Adams', group: 'Group 1', avatar: srcs[1] },
          { name: 'Ali Connors', group: 'Group 1', avatar: srcs[2] },
          { name: 'Trevor Hansen', group: 'Group 1', avatar: srcs[3] },
          { name: 'Tucker Smith', group: 'Group 1', avatar: srcs[2] },
          { divider: true },
          { header: 'Group 2' },
          { name: 'Britta Holt', group: 'Group 2', avatar: srcs[4] },
          { name: 'Jane Smith ', group: 'Group 2', avatar: srcs[5] },
          { name: 'John Smith', group: 'Group 2', avatar: srcs[1] },
          { name: 'Sandra Williams', group: 'Group 2', avatar: srcs[3] }
        ],
        title: 'The summer breeze'
      }
    },

    watch: {
      isUpdating (val) {
        if (val) {
          setTimeout(() => (this.isUpdating = false), 3000)
        }
      }
    },

    methods: {
      remove (item) {
        const index = this.friends.indexOf(item.name)
        if (index >= 0) this.friends.splice(index, 1)
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
    background: red;

  .v-autocomplete__content.v-menu__content, .v-autocomplete__content.v-menu__content .v-card
    min-width: auto !important;
</style>
