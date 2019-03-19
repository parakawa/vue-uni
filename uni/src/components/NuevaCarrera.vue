<template lang="pug">
  v-container.justify-center.form-career(fluid)
    v-form.mt-5
      h1 Nueva Carrera
      v-layout.mt-5
        v-flex.xs-6
          label Nombre
          input.input-career(placeholder="Nombre", v-model='name')
        v-flex.xs-6
          label Nº Ciclos
          select(v-model='nCiclos')
            option Seleccione
            option(v-for='i in 10') {{i}}        
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
      Ciclo(v-for='i in nCiclos')
              
</template>

<script>
import Ciclo from './Ciclo'

export default {
  components: {
    Ciclo
  },
  data () {
    return {
      nCiclos: 0,
      name: '',
      code: '',
      facultie: '',
      faculties: ['Matemática', 'Educación'],
    }
  },
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
    width: 5em;
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
</style>
