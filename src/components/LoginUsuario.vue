<template >
<div align="center">

<h1>Esto es un login para prueba del JWT que se implementara luego</h1>

<v-col cols="10"
sm="5"
md="5" >
    <v-text-field  label="Usuario" id="usuario">

    </v-text-field>
</v-col>



<v-col cols="10"
sm="5"
md="5" >
    <v-text-field  label="Clave" id="clave">

    </v-text-field>
</v-col>


<v-btn @click="logeoUsuario">Login</v-btn>

</div>
  
</template>

<script>
export default {

    data(){
      return{
        sesion:false,
        
      }  
    },

methods:{

    async logeoUsuario(){
        
        
        let nombreusuario = document.getElementById('usuario').value;
        let claveusuario = document.getElementById('clave').value; 

        const objeto = {
            nombreUsuario: nombreusuario,
            claveUsuario: claveusuario
        }

        console.log(nombreusuario);
        console.log(claveusuario);
       await fetch("https://crudLibro.somee.com/api/usuario",{
            method: 'POST',
            body: JSON.stringify(objeto),
            headers: {
                'Content-Type':'application/json'
            }
        })
       .then(resp=>resp.json())
       .then(respuesta => {
         this.sesion = respuesta;
        console.log(this.sesion)
       })
         this.$emit('logueo', this.sesion);
    }

}

}
</script>

<style>

</style>