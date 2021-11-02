<template>
    <div class="cont">
        <div>
            <br>
            <Datos/>
            <div>
                <v-banner>
                    <Header/>
                </v-banner>
            </div>
            <div class="text-h4 text-center">
            </div>
            <div class="pa-7">
                <v-data-table :headers="headers" :items="usuariosBD" :items-per-page="5" class="elevation-5" >
                    <template #[`item.editar`]="{item}">
                    <v-btn color="#66BB6A" fab x-small @click="editarUsuario(item.id)">
                            <v-icon>
                            mdi-account-edit 
                            </v-icon>
                        </v-btn>  
                    </template>
                    <template #[`item.borrar`]="{item}">
                    <v-btn color="#EF5350" fab x-small @click="guardarUsuario(item.id)">
                            <v-icon>
                            mdi-trash-can 
                            </v-icon>
                        </v-btn>  
                    </template>
                </v-data-table>

                <v-row justify="center">
                <v-dialog
                v-model="dialog"
                persistent
                max-width="290"
                >
                    <v-card
                        class="mx-auto"
                        max-width="344"
                    >
                        <v-img
                        src="https://d1csarkz8obe9u.cloudfront.net/posterpreviews/warning-symbol%2C-warning-sign-design-template-5becb2f6646d14a8076b36a92efb1db8_screen.jpg?ts=1609018489"
                        height="200px"
                        ></v-img>

                        <v-card-title>
                        Estas seguro?
                        </v-card-title>
                        
                        <v-card-subtitle>
                        No se podran recuperar los datos
                        </v-card-subtitle>

                        <v-spacer></v-spacer>
                    <v-card-actions>
                    <v-btn
                        color="#66BB6A"
                        text
                        @click="dialog = false"
                    >
                        Cancelar
                    </v-btn>
                    <v-btn
                        color="#EF5350"
                        text
                        @click="borrarUsuario(usuarioId)"
                    >
                        Borrar
                    </v-btn>
                    <br>
                    </v-card-actions>
                </v-card>
                </v-dialog>
            </v-row>
            </div>
            <div>
            
            <Footer/>
            </div>
        </div>
    </div>
</template>

<script>
import vuex from 'vuex'
import Header from './Header.vue'
import Datos from './Datos.vue'
export default {
    components:{
        Datos,
        Header
    },
    data(){
        return{
            usuariosBD: [],
            headers: [
                {text: 'ID', value: 'id', align: 'center', sortable: false},
                {text: 'NOMBRE', value: 'nombre', align: 'center', sortable: false},
                {text: 'CORREO', value: 'correo', align: 'center', sortable: false},
                {text: 'EDITAR', value: 'editar', align: 'center', sortable: false},
                {text: 'BORRAR', value: 'borrar', align: 'center', sortable: false},
            ],
            itemsBD: [],
            dialog: false,
        }
    },
    created: function(){
        this.consultarUsuarios()
    },
    methods: {
        consultarUsuarios(){
            fetch('http://localhost/')
            .then(respuesta => respuesta.json())
            .then((datosRespuesta) => {
                this.usuariosBD = []
                if(typeof datosRespuesta[0].success === 'undefined'){
                    this.usuariosBD = datosRespuesta
                    this.usuariosBD.forEach(item => {
                        console.log(item)
                    })
                    console.log(this.usuariosBD)
                }
            })
            .catch(console.log)
        },
        editarUsuario(id){
            this.$store.commit('setIdUsuario', id)
            window.location.href = "/editar"
        },
        borrarUsuario(usuarioId){
            console.log(usuarioId)
            fetch('http://localhost/?borrar='+usuarioId)
            .then( respuesta => respuesta.json)
            .then( (datosRespuesta) => {
                this.usuarioId  = null
                window.location.href = "listar"
            })
        },
        guardarUsuario(id){
            this.usuarioId = id
            this.dialog = true
        }
    }
    
}
</script>

<style scoped>

.cont{
    min-height: calc(100vh - 2px - 70px);
}

</style>    