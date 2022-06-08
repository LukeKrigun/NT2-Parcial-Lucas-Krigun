<template>

  <section class="src-components-notas">
    <div class="jumbotron">
      <h2><i>notas de alumnos</i></h2>
      <hr>
      <br>

      <vue-form :state="formstate" @submit.prevent="enviar()">
        
       
        <validate tag="div">
          <label for="nombre">Nombre</label>
          <input type="text" id="nombre" v-model="formData.nombre" required name="nombre" autocomplete="off"  class="form-control"
          :minlength="caracterMinLength"
          :maxlength="caracterMaxLength"
          no-espacios
          />

          
         <field-messages name="nombre" show="$dirty">
            
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
            <div slot="minlength" class="alert alert-danger mt-1">
              Este campo requiere como mínimo {{caracterMinLength}} caracteres.
            </div>
            
            <div class="alert alert-danger mt-1" v-if="formData.nombre.length==caracterMaxLength">
              Alcanzaste el máximo de {{caracterMaxLength}} caracteres permitidos.
            </div>

            <div slot="no-espacios" class="alert alert-danger mt-1">
              No se permiten espacios intermedios en este campo.
            </div>
          </field-messages>
        </validate>
        <br>
 
        <validate tag="div">
          <label for="nombre">Apellido</label>
          <input type="text" id="apellido" v-model="formData.apellido" required name="apellido" autocomplete="off" class="form-control"
          :minLength="caracterMinLength"
          :maxlength="caracterMaxLength"
          no-espacios
          />
    

         <field-messages name="apellido" show="$dirty">
           
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
            <div slot="caracterMinLength" class="alert alert-danger mt-1">
              Este campo requiere como mínimo {{caracterMinLength}} caracteres.
            </div>
            
            <div class="alert alert-danger mt-1" v-if="formData.apellido.length==caracterMaxLength">
              Alcanzaste el máximo de {{caracterMaxLength}} caracteres permitidos.
            </div>

            <div slot="no-espacios" class="alert alert-danger mt-1">
              No se permiten espacios intermedios en este campo.
            </div>
          </field-messages>
        </validate>
        <br>
       
        
     
        <validate tag="div">
          <label for="nota">nota</label>
          <input type="number" id="nota" v-model.number="formData.nota" required name="nota" autocomplete="off" class="form-control"
            :min="notaMin"
            :max="notaMax"
          />
    <field-messages name="nota" show="$dirty">
      
            <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
            <div slot="min" class="alert alert-danger mt-1">
               La nota no puede ser menor a {{notaMin}}.
            </div>
            <div slot="max" class="alert alert-danger mt-1">
              La nota no puede ser mayor a {{notaMax}}.
            </div>
      
          </field-messages>
        </validate>
        <br>

        <button class="btn btn-success my-3" :disabled="formstate.$invalid" type="submit">Enviar</button>
      </vue-form>
      <br>
      <hr>

    
      <h2><i>Detalle de alumnos</i></h2>
      <br>

      

      <div v-if="alumnos.length" class="table-responsive">
        <table class="table">
          <tr>
            <th>Nombre</th>
            <th>Apellido</th>
            <th>nota</th>
           
          </tr>
          <tr v-for="(alumno,index) in alumnos" :key="index" :style="{color: analizarNota(alumno).color }">
            <td>{{ alumno.nombre }}</td>
            <td>{{ alumno.apellido }}</td>
            <td>{{ alumno.nota }}</td>

          </tr>
        </table>

        
      </div>
      <h3 v-else class="alert alert-info">No hay alumnos ingresados</h3>
    
    </div>
   
    
  </section>

</template>

<script>

  export default  {
    name: 'src-components-notas',
    props: [],
    mounted () {

    },
    data () {
      return {
        formstate : {},
        formData : this.getInitialData(),
        alumnos : [],
        caracterMinLength : 3,
        caracterMaxLength : 15,
        notaMin : 0,
        notaMax : 10,
        notas : []
      }
    },
    methods: {
      getInitialData() {
        return {
          nombre : '',
          apellido: '',
          nota: null
        }
      },
      enviar() {
        let alumno = {...this.formData}

        console.log(alumno)
        this.alumnos.push(alumno)

        this.formData = this.getInitialData()
        this.formstate._reset()
      },
      analizarNota(alumno) {
        let total = alumno.nota
        this.notas.push(total)
        let color = '#080'
        if(total >=0 && total<=3 ) color = 'red'
        if(total >=4 && total<=6) color = 'yellow'
        if(total > 6) color = 'green'
        return {
          valor : total,
          color
        }
      }
    },
    Promedio(){
        let promedio=0
        let sum=0
        let acumulador=0
        for (let index = 0; index < this.notas.length; index++) {
          const element = this.notas[index];
          sum+=element.nota;
          acumulador++;
        }
        promedio=sum/acumulador
        return{
          promedio
        }
      },

    computed: {
    }
}


</script>

<style scoped lang="css">
  .src-components-notas {

  }

  .jumbotron {
    background-color: #7f7c7c;
    color: rgb(25, 19, 19);
    border: 2px inset rgb(0,0,0,0.5);
  }

  hr {
    background-color: #999;
  }

  label {
    font-weight: bold;
  }

  pre {
    color: white; 
  }
</style>
