<template>
<div class="pa-2">
        <Datos/>
      <div class="cont">
       <v-banner>
            <HeaderCreate/>
       </v-banner>
      <div class="text-h4 text-center pa-1">
      </div>
      <div class="pa-7">
      <v-form
       ref="form"
        v-model="valid"
        lazy-validation
        class="pa-4 elevation-2"
      >
      <v-text-field
        v-model="name"
        :counter="100"
        :rules="nameRules"
        label="Name"
        required
      ></v-text-field>

      <v-text-field
        v-model="email"
        :rules="emailRules"
        label="E-mail"
        required
      ></v-text-field>

      <v-btn
        color="success"
        class="mr-4"
        @click="guardar"
      >
        <v-icon left>
            mdi-content-save
        </v-icon>
          Crear usuario
      </v-btn>
      
      <v-btn
        color="error"
        class="mr-4"
        @click="reset"
      >
        <v-icon left>
            mdi-eraser-variant
        </v-icon>
          Reiniciar formulario
      </v-btn>
    </v-form>
    </div>
    <v-dialog
              v-model="dialog"
              persistent
              max-width="290"
            >
               <v-card
                color=success
               >
                  <v-alert type="success">
                  Usuario creado correctamente
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
import HeaderCreate from './HeaderCreate.vue'
  export default {
    components:{
        Datos,
        HeaderCreate
    },
    data: () => ({
      valid: true,
      dialog: false,
      name: '',
      nameRules: [
        v => !!v || 'Name is required',
        v => (v && v.length <= 100) || 'Name must be less than 100 characters',
      ],
      email: '',
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
      ],
        usuario: {}
    }),
    methods: {
      guardar(){
        var datosUsuario = {
            nombre: this.name,
            correo: this.email
        }
        console.log(datosUsuario)
        fetch('http://localhost/?insertar=1',{
            method: "POST",
            body: JSON.stringify(datosUsuario)
        })
        .then(respuesta => respuesta.json())
        .then(( datosRespuesta =>{
            console.log(datosRespuesta)
            this.reset()
            this.dialog = true
        }))
      },
        reset () {
          this.$refs.form.reset()  
      }
    },
  }
</script>

<style scoped>
.cont{
    min-height: calc(100vh - 66px - 70px);
}
</style>