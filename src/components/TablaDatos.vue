<template>
  <div>
    <h1 align="center">TablaDatos</h1>
    
    
    <div v-if="redirigir == false">
      <div align="right">
        <v-btn align="center" color="green"><v-icon  color="white" @click="agregarLibroView()" align="center">mdi-plus</v-icon></v-btn>
        <br>
        <br>
      </div>
  <v-card>
    <v-card-title>
      <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Search"
        single-line
        hide-details
      ></v-text-field>
    </v-card-title>
    <v-data-table
      :headers="headers"
      :items="libros"
      :search="search" 
       
    >
    <template v-slot:[`item.action`]="{ item }">
        <v-icon
        small
        color="blue"
        class="mr-2"
        @click="editarLibroView(item)">mdi-pencil</v-icon>
        <v-icon
        samall
        color="red"
        @click="eliminarLibroView(item)">mdi-delete</v-icon>
    </template>
    </v-data-table>
  </v-card>
    </div>
     <AgregarLibro @regresar="redirigir = $event" v-else-if="agregar==true"  />
    <EditarLibro @regresar="redirigir = $event"  v-else-if="editar==true" v-bind:dataId1="idLibro" />
    <EliminarLibro @regresar="redirigir = $event" v-else-if="eliminar == true"  v-bind:dataId2="idLibro2" v-bind:activador="eliminar"/>
  </div>

   
</template>

<script>
import AgregarLibro from '../components/AgregarLibro.vue';
import EditarLibro from '../components/EditarLibro.vue';
import EliminarLibro from '../components/EliminarLibro.vue';


export default {


components:{

AgregarLibro,
EditarLibro,
EliminarLibro,



},

data (){

return{

    search: '',
    headers:[
        {
            text: "Numero",
            align: 'start',
            filterbase: false,
            value: 'numero',    
        },

        {text: 'Nombre', value: 'nombre'},
        {text: 'Genero', value: 'genero'},
        {text: 'Autor', value: 'autor'},
        {text: 'Año pub.', value: 'anio__publicacion'},
        {text: 'Editorial', value: 'editorial'},


        {
            text:'', value:'action', sortable: false
        }
        

    ],
    libros: [],

    agregar: false,
    editar: false, 
    eliminar: false,
    redirigir: false,
    idLibro:[],
    idLibro2:[],
    activator: false
}

},

methods:{

agregarLibroView(){
          this.agregar = true;
          this.editar = false;
          this.eliminar = false;
          this.redirigir = true
          

          return true;
      },

      editarLibroView(item){
        this.editar = true;
        this.agregar = false;
        this.eliminar = false;
        this.redirigir = true;
        
        this.idLibro = [item];

        console.log(this.idLibro);
        return true;
      },

      eliminarLibroView(item){
        this.eliminar = true;
        this.agregar = false;
        this.editar = false;
        this.redirigir = true;
        this.idLibro2 = [item];
        
        return true;

      },

      
    
},

mounted(){
        fetch("https://crudLibro.somee.com/api/libro")
        .then(respuesta => respuesta.json())
        .then(response => {
            this.libros = response;
            
        })

        
    },

     updated(){

      fetch("https://crudLibro.somee.com/api/libro")
          .then(respuesta => respuesta.json())
          .then(response => {
            this.libros = response;
            
          })
          
          

      }

}
</script>

<style>

</style>