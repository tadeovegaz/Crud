<template>
    <div class="pa-2">
    <Datos/>
     <div class="cont">
        <v-banner>
            <HeaderEditar/>
       </v-banner>
    <v-form
        ref="form"
        v-model="valid"
        lazy-validation
        class="pa-10"
        >
        <v-text-field
        v-model="usuario.nombre"
        :counter="100"
        :rules="nameRules"
        label="Name"
        required
        ></v-text-field>

        <v-text-field
        v-model="usuario.correo"
        :rules="emailRules"
        label="E-mail"
        required
        ></v-text-field>

        <v-btn
        color="success"
        class="mr-4"
        @click="modificarUsuario"
        >
        <v-icon left>
            mdi-content-save
        </v-icon>
            Actualizar usuario
        </v-btn>
        <v-btn
        color="error"
        class="mr-4"
        @click="goHome"
        >
        <v-icon left>
            mdi-eraser-variant
        </v-icon>
            Cancelar
        </v-btn>
    </v-form>
    <v-dialog
              v-model="dialog"
              persistent
              max-width="290"
            >
               <v-card
                color=success
               >
                  <v-alert type="success">
                  Usuario editado 
               </v-alert>
                <v-card-actions>
                  <v-btn
                    block
                    center
                    color="#"
                    text
                    onclick="window.location.href='listar'"
                  >
                  Listo
                  </v-btn>
                </v-card-actions>
                </v-card>
        </v-dialog>
    </div>
    </div>


</template>

<script>
import Datos from './Datos.vue'
import HeaderEditar from './HeaderEditar.vue'
  export default {
    components:{
        Datos,
        HeaderEditar
    },
    data: () => ({
      name: '',
      dialog: false,
      nameRules: [
        v => !!v || 'Name is required',
        v => (v && v.length <= 100) || 'Name must be less than 10 characters',
      ],
      email: '',
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
      ],
      usuario: []
    }),

    methods: {
        goHome () {
        
            window.location.href = 'listar'
        },
            modificarUsuario(){
            let that = this
            fetch('http://localhost/?actualizar='+that.usuario.id,{
                method:"POST",
                body: JSON.stringify(that.usuario)
            })
            .then( respuesta => respuesta.json())
            .then ((datos => {
                console.log(datos)
                this.dialog = true
            }))
        },
            obtenerUsuario(){
            //console.log(this.idUsuario)
            fetch('http://localhost/?consultar='+this.idUsuario)
            .then( respuesta => respuesta.json())
            .then((datos) =>{
                this.usuario = datos[0]
                console.log('usuario', this.usuario)
            })
        }
    },
    mounted() {
        this.obtenerUsuario()
    },
    computed: {
        idUsuario: {
            get(){
                return this.$store.state.idUsuario
            }
        }
    }
  }
</script>
<style scoped>

.cont{
    min-height: calc(100vh - 66px - 70px);
}
</style>