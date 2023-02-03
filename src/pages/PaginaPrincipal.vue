<template>
<div>
<LoginUsuario v-if="sesion == false" @logueo="sesion = $event"/>
<TablaDatos v-else/>
</div>

</template>
<script>

import TablaDatos from '../components/TablaDatos.vue';
import LoginUsuario from '../components/LoginUsuario.vue';

export default {

components:{
    TablaDatos,
    LoginUsuario
},

data(){
    return{
        sesion: false
    }
}

}
</script>

<style>

</style>