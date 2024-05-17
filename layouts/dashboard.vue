<template>
  <v-app>
    <v-navigation-drawer
      app
      permanent
      color="#FFDEC8"
    >
      <v-sheet
        color="#FFDEC8"
        class="pa-2 ma-2"
      >
        <v-img
          :width="210"
          :height="210"
          :src="require('@/assets/images/logo.svg')" />
      </v-sheet>
      <v-list>
        <v-list-item
          v-for="[icon, text, ruta] in links"
          :key="icon"
          link
          :to="ruta"
        >
          <v-list-item-icon>
            <v-icon>{{ icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ text }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
      <div
        class="d-flex align-center justify-space-around"
      >
        <v-avatar>
          <v-img
            alt="John"
            :src="require('@/assets/images/kike.jpg')"
          />
        </v-avatar>
      </div>
      <div class="d-flex align-center justify-space-around">Enrique Perez Gallardo</div>
    </v-navigation-drawer>

    <v-main>
      <v-container class="py-20 px-18" fluid>
        <Nuxt />
      </v-container>
      <v-container>
        <div>Doctors</div>
        <div>'</div>
        <div class="d-flex align-center justify-space-around">
          <v-avatar>
            <v-img
              alt="House"
              :src="require('@/assets/images/house.jpg')"
            />
          </v-avatar>
          <div>House</div>
          <v-avatar>
            <v-img
              alt="Stephen"
              :src="require('@/assets/images/stephen.jpg')"
            />
          </v-avatar>
          <div>Stephen</div>
          <v-avatar>
            <v-img
              alt="Grey"
              :src="require('@/assets/images/grey.jpg')"
            />
          </v-avatar>
          <div>Grey</div>
        </div>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    drawer: null,
    links: [
      ['mdi-account', 'Usuarios', '/dashboard/usuarios'],
      ['mdi-calendar', 'Schedule', '/dashboard/schedule'],
      ['mdi-bed', 'Patients', '/dashboard/patients'],
      ['mdi-cart-outline', 'Orders', '/dashboard/orders']
    ]
  })
}
</script>
