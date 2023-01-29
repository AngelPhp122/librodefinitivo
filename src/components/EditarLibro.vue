<template>
<div>
  <h1>Componente editar libro</h1>

  <v-card >
            <v-card-title align="Center">
              <span class="text-h5" align="Center">Editando libro >>> Numero {{dataId1[0].numero}}  {{dataId1[0].nombre}}</span>
            </v-card-title>

            <v-card-text>
                <v-container>
                    <v-row>
                     
                        <v-col cols="12"
                    sm="6"
                    md="4">
                    <v-text-field label="Nombre" id="Nombre" v-bind:value="dataId1[0].nombre"></v-text-field>
                        </v-col>
                        <v-col cols="12"
                    sm="6"
                    md="4">
                    <v-text-field label="Genero" id="Genero" v-bind:value="dataId1[0].genero"></v-text-field>
                        </v-col>
                        <v-col cols="12"
                    sm="6"
                    md="4">
                    <v-text-field label="Autor" id="Autor" v-bind:value="dataId1[0].autor"></v-text-field>
                        </v-col>
                        <v-col cols="10"
                    sm="1"
                    md="4">
                    
      <v-menu
        ref="menu"
        v-model="menu"
        :close-on-content-click="false"
        :return-value.sync="date"
        transition="scale-transition"
        offset-y
        min-width="auto"
      >
        <template v-slot:activator="{ on, attrs }">
          <v-text-field
            v-model="date"
            label="Picker in menu"
            prepend-icon="mdi-calendar"
            readonly
            v-bind="attrs"
            v-on="on"

            id="fecha"
          ></v-text-field>
        </template>
        <v-date-picker
          v-model="date"
          no-title
          scrollable
        >
          <v-spacer></v-spacer>
          <v-btn
            text
            color="primary"
            @click="menu = false"
          >
            Cancel
          </v-btn>
          <v-btn
            text
            color="primary"
            @click="$refs.menu.save(date)"
          >
            OK
          </v-btn>
        </v-date-picker>
      </v-menu>
    </v-col>
                        <v-col cols="12"
                    sm="6"
                    md="4">
                    <v-text-field label="Editorial" id="Editorial" v-bind:value="dataId1[0].editorial"></v-text-field>
                        </v-col>
                    </v-row>
                    <v-row>
                        <v-dialog
                        v-model="dialog"
                        persistent
                        max-width="320">
                        <template 
                        v-slot:activator="{on, attrs}">
                        <v-col align="Center">
                            <v-btn color="green" v-bind="attrs" v-on="on"><v-icon>mdi-check-circle</v-icon></v-btn>
                            <v-btn color="red"  @click="regresarTabla"><v-icon >mdi-close-thick</v-icon></v-btn>
                        </v-col>
                        </template>
                        <v-card>
                            <v-card-title class="text-h5">
                                Desea guardar este libro nuevo?
                            </v-card-title>
                            <v-card-text>
                                Al confirmar, estara guardando en la Base de datos este registro.
                            </v-card-text>
                            <v-card-actions>
                                <v-spacer></v-spacer>
                                <v-btn 
                                color="green darken-1"
                                text
                                @click="actualizarData">
                                Aceptar
                                </v-btn>
                                <v-btn 
                                color="red darken-1"
                                text
                                @click="regresarTabla">
                                cancelar
                                </v-btn>
                            </v-card-actions>
                        </v-card>
                        </v-dialog>
                    </v-row>
                </v-container>
            </v-card-text>
                            

</v-card>

</div>
</template>

<script>
export default {


props:['dataId1'],

data(){
    return{
        dialog: false,
        redirigir: false,
        date: (new Date(Date.now() - (new Date()).getTimezoneOffset() * 60000)).toISOString().substr(0, 10),
      menu: false,
    }
},

methods:{
    actualizarData(){

            
        const dataDeInputs = [{
                               numero:this.dataId1[0].numero, 
                               nombre:document.getElementById('Nombre').value,
                               genero:document.getElementById('Genero').value,
                               autor:document.getElementById('Autor').value,
                               anio__publicacion:document.getElementById('fecha').value,
                               editorial: document.getElementById('Editorial').value}];

        //console.log(dataDeInputs);

        fetch("https://crudLibro.somee.com/api/libro",{
            method:'PUT',
            body:JSON.stringify(...dataDeInputs),
            headers:{
                'Content-Type':'application/json'
            }
        })
        .then(resp=>resp.json())
        .then(console.log);

        this.$emit('regresar', this.redirigir);

    },

    regresarTabla(){

        this.$emit('regresar', this.redirigir);
    }
}


}


</script>

<style>

</style>