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
            username: nombreusuario,
            password: claveusuario
        }

        console.log(nombreusuario);
        console.log(claveusuario);
       await fetch("https://crudLibro.somee.com/api/usuario",{
            method: 'POST',
            body: JSON.stringify(objeto),
            headers: {
                'Access-Control-Allow-Origin':'*',
                'Content-Type':'application/json',
                'Authorization': 'Bearer Token'
            }
        })
       .then(resp=>resp.text())
       .then(respuesta => {

        if(respuesta != null){

            let token = respuesta;
            console.log(token);
            localStorage.setItem("token",token)
            
            this.sesion = true;
            console.log(this.sesion)
        }else{

            console.log(false);
        }
         
       })
         this.$emit('logueo', this.sesion);
    }

}

}
</script>

<style>

</style>