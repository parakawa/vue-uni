<template lang="pug">
    v-card.pa-4.mt-5
        h3 Ciclo {{numeroCiclo + 1}}
        v-autocomplete(v-model='courses', :disabled='isUpdating', :items='optionCourses', chips='', color='', box='', placeholder='Agregar curso a ciclo' item-value='item', multiple='')
          template(v-slot:selection='data')
            v-chip.chip--select-multi(:selected='data.selected', color='primary', text-color='white' close='', @input='remove(data.item)')
              |{{ data.item.name }}
          template(v-slot:item='data')
            template(v-if="typeof data.item !== 'object'")
              v-list-tile-content(v-text='data.item')
            template(v-else='')
              v-list-tile-content
                v-list-tile-title(v-html='data.item.name')
</template>

<script>
export default {
    props: ['numeroCiclo'],
    data () {
      return {
        autoUpdate: true,
        courses: [],
        isUpdating: false,
        optionCourses: [
          { header: 'Group 1' },
          { name: 'Sandra Adams', group: 'Group 1' },
          { name: 'Ali Connors', group: 'Group 1'},
          { name: 'Trevor Hansen', group: 'Group 1' },
          { name: 'Tucker Smith', group: 'Group 1'},
        ],

      }
    },

    methods: {
      remove (item) {
        const index = this.courses.indexOf(item)
        if (index >= 0) this.courses.splice(index, 1)
      }
    },
    watch: {
        courses() {
            this.$emit('cicleChange', { courses: this.courses, index: this.numeroCiclo })
        }
    }
  }
</script>

<style lang="sass">
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