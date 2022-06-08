<template>

  <section class="src-components-respuestas">
    <div class="jumbotron">
      <h2><i>Respuestas</i></h2>

      <div class="table-responsive">
        <table class="table table-dark">
          <tr>
            <th>Numero de Pregunta</th>
            <th>Respuesta</th>
          </tr>
          <tr>
            <td>1</td>
            <td>c</td>
          </tr>
          <tr>
            <td>2</td>
            <td>c</td>
          </tr>
          <tr>
            <td>3</td>
            <td>b</td>
          </tr>
        </table>
      </div>      

    </div>
  </section>

</template>

<script>

  export default  {
    name: 'src-components-respuestas',
    props: [],
    mounted () {

    },
    data () {
      return {

      }
    },
    methods: {

    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-components-respuestas {

  }

  .jumbotron {
    background-color: rgb(166, 90, 196);
    color: #222;
  }
</style>
