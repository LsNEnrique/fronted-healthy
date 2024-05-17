<template>
  <v-card rounded color="#EC9143" class="pa-7" style="height: 70%!important">
    <v-card-title>
      <v-row class="rowCard fontTitle" align="center">
        Welcome
      </v-row>
      <v-row class="rowCard fontTitle" align="end">
        Back
      </v-row>
    </v-card-title>
    <v-card-text>
      <v-row>
        <v-text-field v-model="email" rounded label="E-mail" outlined />
      </v-row>
      <v-row>
        <v-text-field v-model="password" rounded label="Password" outlined />
      </v-row>
    </v-card-text>
    <v-card-actions>
      <v-col cols="12">
        <v-row class="rowCard">
          <v-btn block class="pa-2" color="#134700" @click="login">
            <span style="text-transform:none; color:white;"> Log-In </span>
          </v-btn>
        </v-row>
        <v-row class="rowCard">
          <span>If you dont have and account</span>
          <a @click="showDialog = true"> Sign-Up </a>
        </v-row>
      </v-col>
    </v-card-actions>
    <v-dialog
      v-model="showDialog"
      persistent
      width="500"
      transition="dialog-bottom-transition"
    >
      <v-card>
        <v-card-title>Agregar Usuario</v-card-title>
        <v-card-text>
          <v-row width="100%">
            <v-text-field
              v-model="emailNuevo"
              class="pa-2 ma-2"
              label="Correo"
              placeholder="Escribe tu correo"
              outlined
            />
          </v-row>
          <v-row width="100%">
            <v-text-field
              v-model="passwordNuevo"
              class="pa-2 ma-2"
              label="Password"
              placeholder="Escribe tu Password"
              outlined
              type="password"
            />
            <v-row width="100%">
              <v-text-field
                v-model="nombre"
                class="pa-2 ma-2"
                label="Nombre"
                placeholder="Escribe tu Nombre"
                outlined
              />
              <v-row width="100%">
                <v-text-field
                  v-model="apaterno"
                  class="pa-2 ma-2"
                  label="A. Paterno"
                  placeholder="Escribe tu A. Paterno"
                  outlined
                />
              </v-row>
              <v-row width="100%">
                <v-text-field
                  v-model="amaterno"
                  class="pa-2 ma-2"
                  label="A. Materno"
                  placeholder="Escribe tu A. Materno"
                  outlined
                />
                <v-row width="100%">
                  <v-text-field
                    v-model="direccion"
                    class="pa-2 ma-2"
                    label="Direccion"
                    placeholder="Escribe tu direccon"
                    outlined
                  />
                  <v-row width="100%">
                    <v-text-field
                      v-model="telefono"
                      class="pa-2 ma-2"
                      label="Telefono"
                      placeholder="Escribe tu telefono"
                      outlined
                    />
                  </v-row>
                </v-row>
              </v-row>
            </v-row>
          </v-row>
        </v-card-text>
        <v-card-actions>
          <v-col cols="6">
            <v-btn block color="green" @click="registrarUsuario">
              <span style="text-transform: none; color: white">
                Registrar
              </span>
            </v-btn>
          </v-col>
          <v-col cols="6">
            <v-btn block color="red" @click="showDialog = false">
              <span style="text-transform: none; color: white">
                Cancelar
              </span>
            </v-btn>
          </v-col>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-card>
</template>

<script>
export default {
  data () {
    return {
      email: null,
      password: null,
      showDialog: false,
      emailNuevo: null,
      passwordNuevo: null,
      nombre: null,
      apaterno: null,
      amaterno: null,
      direccion: null,
      telefono: null
    }
  },
  methods: {
    async login () {
      await console.log('@@@ datos => ', this.email, this.password)
      const sendData = {
        email: this.email,
        password: this.password
      }
      await this.$auth.loginWith('local', {
        data: sendData
      }).then(async (res) => {
        const result = await res.data
        if (result.message === 'success') {
          this.$store.commit('setToken', result.token)
          this.$router.push('/dashboard')
        }
      }).catch((err) => {
        console.log('@@@ error => ', err)
      })
    },
    registrarUsuario () {
      const url = '/register'
      const data = {
        nombre: this.nombre,
        apaterno: this.apaterno,
        amaterno: this.amaterno,
        direccion: this.direccion,
        telefono: this.telefono,
        email: this.emailNuevo,
        password: this.passwordNuevo
      }
      this.$axios.post(url, data)
        .then((res) => {
          console.log('@@ res => ', res)
        })
        .catch((error) => {
          console.log('@@ error => ', error)
        })
    }
  }
}
</script>

<style scoped>
.rowCard{
  width: 100%;
  display: flex;
  justify-content: center;
}
.fontTitle{
  font-size: 52px!important;
  line-height: 78px!important;
}

</style>
