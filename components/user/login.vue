<template>
    <v-card class="cardLogin">
        <v-card-title class="title">Bienvenidos</v-card-title>
        <v-card-text>
            <v-row justify="center" align="center">
                <v-col cols="4" align-self="center">
                    <img src="../../assets/images/c.jpg" class="imgLogin">
                </v-col>
                <v-col cols="8" align-self="center">
                    <v-form ref="formLogin">
                <v-text-field label="Correo Electronico" 
                              placeholder="Correo Electronico"
                              v-model="correoElectronico"
                              :rules="validarCorreo"
                />
                <v-text-field label="Contraseña" 
                              placeholder="Contraseña"
                              v-model="password"
                              :rules="validarPassword"
                />

            </v-form>
                </v-col>
            </v-row>

        
            
        </v-card-text>
        <v-card-actions class="papito">
            <v-btn
            class="btnLogin"
            rounded
            flex
            @click="loginBackend"
            >
                Iniciar
            </v-btn>
            <v-btn
            class="btnCreateAcount"
            flex
            @click="loginBackend"
            >
            ¿No tienes una cuenta? ¡crea una ya!
            </v-btn>
        </v-card-actions>

    </v-card>
</template>

<script>
export default {
    data() {
        return {
            correoElectronico: '',
            validarCorreo: [
            v => !v || /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(v) || 'Correo no valido'
            ],
            password:'',
            validarPassword: [
                value => value.length >= 6 || 'Minimo 6 caracteres'
            ]
        }
    },
    methods: {
        async loginBackend () {
            const valid = this.$refs.formLogin.validate()
            if (valid) {
                const sendData = {
                    email: this.correoElectronico,
                    password: this.password
                }
                await this.$auth.loginWith('local', {
                    data: sendData
                }).then(async (res) => {
                    console.log('respuesta del back:', res)
                    if (res.data.error == null) {
                        this.$router.push('/dashboard')
                    }
                }).catch((error) => {
                    console.log('error: ', error)
                })
            }else {
                alert('no cumpliste las reglas')
            }
        }
    }
}
</script>

<style scoped>
    .cardLogin{
        font-family:'Courier New', Courier, monospace;
        background-color: #f651cd8f;
        border-radius: 10px;
        width: 500px;
        height: 350px;
    }
    .imgLogin {
        width: 100%;
        height: 100%;
    }
    .btnLogin{
        background-color: #ca006fe7!important;
        color: #FFFFFF;
        width: 100%;
    }
    .btnCreateAcount{
        background-color: #ffffff00!important;
        color: #92e9ff;
    }
    .title {
        font-family: Verdana, Geneva, Tahoma, sans-serif;
        font-size: 30px;
        justify-content: center;
        color: #3a3538;
        font-weight: 700;
    }
    .papito {
        display: flex;
        flex-direction: column;
    }
</style>