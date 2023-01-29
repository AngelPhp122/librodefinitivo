<template>
<div>
  <h1 align="Center">Componente agregar</h1>

<v-card >
            <v-card-title align="Center">
              <span class="text-h5" align="Center">Agregando nuevo libro</span>
            </v-card-title>

            <v-card-text>
                <v-container>
                    <v-row>
                        <v-col cols="1"
                    sm="1"
                    md="2">
                    <v-text-field label="Numero" id="Numero" type="number"></v-text-field>
                        </v-col>

                        <v-spacer></v-spacer>
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
    
                    

                    </v-row>
                    <v-row>
                         <v-col cols="2"
                    sm="5"
                    md="3">
                    <v-text-field label="Autor" id="Autor"></v-text-field>
                        </v-col>
                    <v-spacer></v-spacer>
                    <v-col
                    cols="10"
                    sm="6"
                    md="4"
                    >
                    <v-text-field label="Editorial" id="Editorial"></v-text-field>
                        </v-col>
                    </v-row>
                    <v-row>
                        <v-col cols="10"
                    sm="1"
                    md="3">
                    <v-text-field label="Nombre" id="Nombre"></v-text-field>
                        </v-col>
                    </v-row>
                    <v-row>
                        <v-col cols="10"
                    sm="1"
                    md="3">
                    <v-text-field label="Genero" id="Genero"></v-text-field>
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
                            <v-btn color="red"  @click="cancelarIngreso"><v-icon >mdi-close-thick</v-icon></v-btn>
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
                                @click="guardarData">
                                Aceptar
                                </v-btn>
                                <v-spacer></v-spacer>
                                <v-btn 
                                color="red darken-1"
                                text
                                @click="cancelarIngreso">
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

data(){
    return {
        libroNuevo:{
            numero: 0,
      nombre: '',
      genero: '',
      autor: '',
      anio__publicacion: '',
      editorial: ''
        },
        date: (new Date(Date.now() - (new Date()).getTimezoneOffset() * 60000)).toISOString().substr(0, 10),
      menu: false,

        redirigir: false,
        dialog: false,
    }
},


methods:{
    cancelarIngreso(){
        this.$emit('regresar', this.redirigir);
    },

    guardarData(){
        this.libroNuevo.numero = document.getElementById('Numero').value;
        this.libroNuevo.nombre = document.getElementById('Nombre').value;
        this.libroNuevo.genero = document.getElementById('Genero').value;
        this.libroNuevo.autor = document.getElementById('Autor').value;
        this.libroNuevo.anio__publicacion = document.getElementById('fecha').value;
        this.libroNuevo.editorial = document.getElementById('Editorial').value;
        this.dialog = false;

        fetch("https://crudLibro.somee.com/api/libro",{
            method:'POST',
            body: JSON.stringify(this.libroNuevo),
            headers:{
                'Content-Type':'application/json'
            }
        })
        .then(resp=>resp.json())
        .then(console.log)
        this.$emit('regresar', this.redirigir);
        
    }
}

}
</script>

<style>

</style>