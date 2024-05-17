<template>
  <div>
    <v-col cols="12">
      <v-row>
        <v-btn block color="#123CCC" @click="showDialog = true">
          <span style="text-transform: none; color: white;">
            Usuario nuevo
          </span>
        </v-btn>
      </v-row>
      <v-row>
        <v-data-table
          :headers="headers"
          :items="usuarios"
        >
          <template #[`item.email`]="{item}">
            <span style="font-weight: 800;">
              {{ item.email }}
            </span>
          </template>
          <template #[`item.acciones`]="{item}">
            <v-row>
              <v-col cols="6">
                <v-btn icon color="red" @click="deleteUser(item)">
                  <v-icon>mdi-trash-can</v-icon>
                </v-btn>
              </v-col>
              <v-col cols="6">
                <v-btn icon color="warning" @click="updateUser(item)">
                  <v-icon>mdi-account</v-icon>
                </v-btn>
              </v-col>
            </v-row>
          </template>
        </v-data-table>
      </v-row>
      <v-dialog
        v-model="showDialog"
        persistent
        width="500"
        transition="dialog-bottom-transition"
      >
        <v-card>
          <v-card-title>Agregar usuario</v-card-title>
          <v-card-text>
            <v-row width="100%">
              <v-text-field
                v-model="nombre"
                class="pa-2 ma-2"
                label="Nombre"
                placeholder="Escribe tu nombre"
                outlined
                type="nombre"
              />
            </v-row>
          </v-card-text>
          <v-card-text>
            <v-row width="100%">
              <v-text-field
                v-model="apaterno"
                class="pa-2 ma-2"
                label="A. Paterno"
                placeholder="Escribe tu A. paterno"
                outlined
                type="apaterno"
              />
            </v-row>
          </v-card-text>
          <v-card-text>
            <v-row width="100%">
              <v-text-field
                v-model="amaterno"
                class="pa-2 ma-2"
                label="A. Materno"
                placeholder="Escribe tu A. materno🫚"
                outlined
                type="amaterno"
              />
            </v-row>
          </v-card-text>
          <v-card-text>
            <v-row width="100%">
              <v-text-field
                v-model="direccion"
                class="pa-2 ma-2"
                label="Direccion"
                placeholder="Escribe tu direccion"
                outlined
                type="direccion"
              />
            </v-row>
          </v-card-text>
          <v-card-text>
            <v-row width="100%">
              <v-text-field
                v-model="telefono"
                class="pa-2 ma-2"
                label="Telefono"
                placeholder="Escribe tu telefono"
                outlined
                type="Telefono"
              />
            </v-row>
          </v-card-text>
          <v-card-text>
            <v-row width="100%">
              <v-text-field
                v-model="email"
                class="pa-2 ma-2"
                label="Correo"
                placeholder="Escribe tu correo"
                outlined
              />
            </v-row>
          </v-card-text>
          <v-card-text>
            <v-row width="100%">
              <v-text-field
                v-model="password"
                class="pa-2 ma-2"
                label="Password"
                placeholder="Escribe tu contraseña"
                outlined
                type="password"
              />
            </v-row>
          </v-card-text>
          <v-card-actions>
            <v-col cols="6">
              <v-btn block color="green" @click="registrarUsuario">
                <span style="text-transform: none; color: white;">
                  Registrar
                </span>
              </v-btn>
            </v-col>
            <v-col cols="6">
              <v-btn block color="red" @click="showDialog = false">
                <span style="text-transform: none; color: white; ">
                  Cancelar
                </span>
              </v-btn>
            </v-col>
          </v-card-actions>
        </v-card>
      </v-dialog>
      <v-dialog
        v-model="showUpdate"
        persistent
        width="500"
        transition="dialog-bottom-transition"
      >
        <v-card>
          <v-card-title>Actualizar Usuario</v-card-title>
          <v-card-text>
            <v-row width="100%">
              <v-text-field
                v-model="userToUpdate.nombre"
                class="pa-2 ma-2"
                label="Nombre"
                placeholder="Escribe tu Nombre"
                outlined
                type="nombre"
              />
            </v-row>
            <v-row width="100%">
              <v-text-field
                v-model="userToUpdate.apaterno"
                class="pa-2 ma-2"
                label="A. Paterno"
                placeholder="Escribe tu A. Paterno"
                outlined
                type="apaterno"
              />
            </v-row>
            <v-row width="100%">
              <v-text-field
                v-model="userToUpdate.amaterno"
                class="pa-2 ma-2"
                label="A. Materno"
                placeholder="Escribe tu A. Materno"
                outlined
                type="amaterno"
              />
            </v-row>
            <v-row width="100%">
              <v-text-field
                v-model="userToUpdate.direccion"
                class="pa-2 ma-2"
                label="Direccion"
                placeholder="Escribe tu direccon"
                outlined
                type="direccion"
              />
              <v-row width="100%">
                <v-text-field
                  v-model="userToUpdate.telefono"
                  class="pa-2 ma-2"
                  label="Telefono"
                  placeholder="Escribe tu telefono"
                  outlined
                  type="telefono"
                />
              </v-row>
              <v-row width="100%">
                <v-text-field
                  v-model="userToUpdate.email"
                  class="pa-2 ma-2"
                  label="Correo"
                  placeholder="Escribe tu correo"
                  outlined
                />
              </v-row>
              <v-row width="100%">
                <v-text-field
                  v-model="userToUpdate.password"
                  class="pa-2 ma-2"
                  label="Password"
                  placeholder="Escribe tu Password"
                  outlined
                  type="password"
                />
              </v-row>
            </v-row>
          </v-card-text>
          <v-card-actions>
            <v-col cols="6">
              <v-btn block color="green" @click="actualizarUsuario">
                <span style="text-transform: none; color: white;">
                  Registrar
                </span>
              </v-btn>
            </v-col>
            <v-col cols="6">
              <v-btn block color="red" @click="showDialog = false">
                <span style="text-transform: none; color: white; ">
                  Cancelar
                </span>
              </v-btn>
            </v-col>
          </v-card-actions>
        </v-card>
      </v-dialog>
      <v-dialog v-model="showDelete" width="300" persistent>
        <v-card>
          <v-card-title>Delete user</v-card-title>
          <v-card-text>Are you sure?</v-card-text>
          <v-card-actions>
            <v-col cols="6">
              <v-btn block color="green" @click="borrarUsuario">
                <span style="text-transform: none; color: white;">
                  Borrar
                </span>
              </v-btn>
            </v-col>
            <v-col cols="6">
              <v-btn block color="red" @click="showDelete = false">
                <span style="text-transform: none; color: white;">
                  Cancelar
                </span>
              </v-btn>
            </v-col>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-col>
  </div>
</template>

<script>
import { mapState } from 'vuex'
export default {
  layout: 'dashboard',
  auth: true,
  data () {
    return {
      usuarios: [],
      headers: [
        {
          text: 'Nombre',
          value: 'nombre',
          align: 'center',
          sortable: true
        },
        {
          text: 'A. Paterno',
          value: 'apaterno',
          align: 'center',
          sortable: true
        },
        {
          text: 'A. Materno',
          value: 'amaterno',
          align: 'center',
          sortable: true
        },
        {
          text: 'Direccion',
          value: 'direccion',
          align: 'center',
          sortable: true
        },
        {
          text: 'Telefono',
          value: 'telefono',
          align: 'center',
          sortable: true
        },
        {
          text: 'Email',
          value: 'email',
          align: 'center',
          sortable: true
        },
        {
          text: 'Acciones',
          value: 'acciones',
          align: 'center'
        }
      ],
      showDialog: false,
      email: null,
      password: null,
      userToDelete: null,
      showDelete: false,
      nombre: null,
      apaterno: null,
      amaterno: null,
      direccion: null,
      telefono: null,
      userToUpdate: {},
      showUpdate: false
    }
  },
  computed: {
    ...mapState({
      token: state => state.token
    })
  },
  mounted () {
    this.obtenerUsuarios()
  },
  methods: {
    obtenerUsuarios () {
      const url = '/getallusers'
      this.$axios.get(url)
        .then((res) => {
          // console.log('response =>', res)
          if (res.data.message === 'success') {
            this.usuarios = res.data.users
          }
        })
        .catch((error) => {
          console.log('@@@error => ', error)
        })
    },
    registrarUsuario () {
      const url = '/register'
      const data = {
        email: this.email,
        password: this.password,
        nombre: this.nombre,
        apaterno: this.apaterno,
        amaterno: this.amaterno,
        direccion: this.direccion,
        telefono: this.telefono

      }
      this.$axios.post(url, data)
        .then((res) => {
          console.log('@@ res => ', res)
        })
        .catch((error) => {
          console.log('@@ error => ', error)
        })
    },
    borrarUsuario () {
      const url = `/users/${this.userToDelete.email}`
      this.$axios.delete(url)
        .then((res) => {
          if (res.status === 204) {
            this.showDelete = false
            this.obtenerUsuarios()
          }
        })
        .catch((err) => {
          console.log('@@ err => ', err)
        })
    },
    deleteUser (user) {
      this.userToDelete = user
      this.showDelete = true
      console.log('@@@ user => ', this.userToDelete)
    },
    updateUser (user) {
      this.usertoUpdate = user
      this.showUpdate = true
    },
    actualizarUsuario () {
      const url = `/users/${this.userToUpdate.email}`
      this.$axios.put(url, this.userToUpdate)
        .then((res) => {
          if (res.data.message === 'success') {
            this.obtenerUsuarios()
            this.showDelete = false
          }
        })
        .catch((err) => {
          console.log('@@ err => ', err)
        })
    }
  }
}
</script>
