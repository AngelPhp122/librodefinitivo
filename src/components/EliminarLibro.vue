<template v-slot:activator="{ on, attrs }" max-width="20">



    <v-row justify="center">
      <v-dialog
      v-model="dialog"
      persistent
      max-width="400"
      >
       
       <v-card>
        <v-card-title class="text-h5">
          Desea eliminar este libro {{dataId2[0].numero}}?
        </v-card-title>
       

       <v-card-text>
          Si presiona el boton aceptar este libro quedara permanentemente eliminado
       </v-card-text>
       <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn
        color="green darken-3"
        text
        @click="eliminarData">
        Aceptar
        </v-btn>
        <v-btn
        color="red darken-3"
        text
        @click="regresarTabla">
        Cancelar
        </v-btn>
       </v-card-actions>
       </v-card>
      </v-dialog>
    </v-row>

</template>

<script>
export default {

props:

  ['dataId2'],
  

data(){
  return{
    dialog:true,
    redirigir:false,
    indexLibro: 0
  }
},

   methods:{

    eliminarData(){
       
     this.indexLibro = this.dataId2[0].numero

      

    fetch(`http://crudLibro.somee.com/api/libro/${this.indexLibro}`,{
      method: 'DELETE'
      
    })
    this.dialog = false
    this.$emit('regresar', this.redirigir);
    },

    regresarTabla(){
      this.dialog = false
      this.$emit('regresar', this.redirigir);
    }

  }
}


</script>

<style>

</style>