<template lang="pug">
    v-container.justify-center.form-career(fluid)
        v-form.mt-5(@submit.prevent='submit')
            h1 Nueva Carrera
            v-layout.mt-5
                v-flex.xs-6
                    v-text-field(v-model='name', :rules='verifyCarrera', label='Nombre', required='')
                v-flex.xs-6
                    label Nº Ciclos
                    select(v-model='nCiclos')
                        option Seleccione
                        option(v-for='i in 10') {{i}}        
            v-layout.mt-3
                v-flex.xs-6
                    v-text-field(v-model='code', :rules='verifyCode', label='Código', required='')
                v-flex.xs-6
                    v-select(v-model='facultie', :items='faculties', label='Select', :rules='verifyFacultie', required='')
                    //- label Facultad
                    //- select(v-model='facultie' v-model.trim="$v.code.$model")
                    //-     option Seleccione
                    //-     option(v-for='(facultie, i) in faculties' :key="i") {{facultie}}
                    //- .err(v-if="!$v.facultie.required") Field is required
            h2.mt-3.mb-3.blue--text Cursos por carrera
            Ciclo(v-for='(item, i) in Number(nCiclos)' :key="i", :numeroCiclo="i" :ref="getRefName(i)" @cicleChange="getCicleInfo") 

        v-dialog(width='500' v-model="dialog")
            template(v-slot:activator='{ on }')
                v-btn(color='red lighten-2', dark='', v-on='on', :disabled='isComplete')
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
                        li(v-for='(course,i) in courses' :key="i")
                            h4 Ciclo {{i+1}}  
                            ol 
                                li(v-for='(item,k) in course ' :key="k") {{item.name}}

</template>

<script>
import Ciclo from './Ciclo'
import { required, minLength, email } from 'vuelidate/lib/validators'

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
            list: [
                { id: 1, name: 'item 1'}
            ],
			dialog: false,
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
          minLength: minLength(4),
          email,
		  },
	    code: {
          required,
		  },
	    facultie: {
          required,
		  },
        },	
        	  		  	  
    computed: {
        faculties() {
            return this.$store.state.faculties;
        },
        newList() {
            let result = this.list.map(item => ({ label: item.name, value: item.id }))
            return result
        },
		isComplete () {
            return !(this.$v.name.required && this.$v.code.required && this.$v.facultie.required);
        },
        verifyCarrera () {
            if(!this.$v.name.required) return ['El nombre es requerido'];
            else if(!this.$v.name.minLength) return ['Debe escribir al menos 4 caracteres'];
            else if(!this.$v.name.email) return ['El campo debe ser email'];
        },
        verifyCode () {
            return [this.$v.code.required || 'El código es requerido'];
        },
        verifyFacultie () {
            return [this.$v.code.required || 'La facultad es requerida'];
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
