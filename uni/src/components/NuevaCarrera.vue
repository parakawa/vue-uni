<template lang="pug">
  v-container.justify-center.form-career(fluid)
    v-form.mt-5(@submit.prevent='submit')
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
            option(v-for='(facultie, i) in faculties' :key="i") {{facultie}}
      h2.mt-3.mb-3.blue--text Cursos por carrera
      Ciclo(v-for='(item, i) in Number(nCiclos)' :key="i", :numeroCiclo="i" :ref="getRefName(i)" @cicleChange="getCicleInfo") 
      template
      .text-xs-center
        v-dialog(width='500')
          template(v-slot:activator='{ on }')
            v-btn(color='red lighten-2', dark='', v-on='on' :disabled='!isComplete')
              | Click Me
          v-card
            v-card-title.headline.grey.lighten-2(primary-title='')
              | Datos
            v-card-text
              p Nombre: {{name}}
              p Código: {{code}}
              p Facultad: {{facultie}}
              p Cursos: 
              ul
                div(v-for='(course,i) in courses')
                  h4 Ciclo {{i+1}}  
                    ol 
                      li(v-for='(item,k) in course[i]') {{item.name}}               
                  
</template>

<script>
import Ciclo from './Ciclo'
import { required, minLength } from 'vuelidate/lib/validators'

export default {
    components: {
        Ciclo
    },
    data () {
        return {
            nCiclos: 3,
            courses: [],
            name: '',
            code: '',
            facultie: '',
            faculties: ['Matemática', 'Educación'],
            list: [
                { id: 1, name: 'item 1'}
            ],
            // referencias: {
            //     name: 'Maritza',
            //     id: '123'
            // }
        }
    },
    methods: {
        getRefName(i) {
            return `cicle-${i}`
        },
        getCicleInfo(val) {
            this.courses[val.index] = val.courses;
        }
    },
    validations: {
        name: {
		  required,
		  minLength: minLength(4)
		  },
	    code: {
          required,
		  },
	    facultie: {
          required,
		  },
		},		  		  	  
    computed: {
        newList() {
            let result = this.list.map(item => ({ label: item.name, value: item.id }))
            return result
        },
        referencias() {
            // let references = []
            // Object.keys(this.refs).forEach(item => {
            //     references.push(this.refs[item])
            // }) 
            // if(this.refs) return Object.keys(this.refs)
        },
        refsCiclos() {
            return 
            
            // [ 'name', 'id' ]
            // Object.keys(this.referencias).forEach(item => {
            //     this.referencias[item]
            // }) 

		},
		isComplete () {
			return this.name && this.code && this.facultie;
		}
    },
    watch: {
        nCiclos() {
            
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
