<template>
  <v-app>
    <v-main>
      <v-sheet
        class="pa-2 ma-2"
        width="100%"
        height="100%"
        color="#FFDEC8"
      >
        <v-row>
          <v-cols cols="6">
            <v-row height="300px" align="center" justify="center">
              <h1>Clinic patients dashboard</h1>
            </v-row>
            <v-row align="center" justify="center">
              <v-img :src="require('@/assets/images/logo.svg')" />
            </v-row>
          </v-cols>
          <v-col cols="6" style="height:">
            <Nuxt />
          </v-col>
        </v-row>
      </v-sheet>
    </v-main>
  </v-app>
</template>
