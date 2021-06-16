<template>
  <v-layout
    column
    justify-center
    align-center
  >
    <v-flex
      xs12
      sm8
      md6
    >
      <v-card>
        <v-card-title class="headline">
          Sistema de reconocimiento facial utilizando TensorFlowJS y face-api-js
        </v-card-title>
        <v-responsive>
          <v-list two-line subheader>
            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>Registro</v-list-item-title>
                <v-list-item-subtitle>Registra la información del usuario</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
            <v-divider />
            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>Sube tus fotografías</v-list-item-title>
                <v-list-item-subtitle>Sube tus fotografías por medio del boton de upload o de la camara.</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
            <v-divider />
            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>Entrenamiento</v-list-item-title>
                <v-list-item-subtitle>Entrena el modelo para que pueda reconocerte.</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
            <v-divider />
            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>Reconocimiento</v-list-item-title>
                <v-list-item-subtitle>Reconoce tu rostro por medio de una camara.</v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
          </v-list>
        </v-responsive>
        <v-card-actions>
          <v-spacer />
          <v-btn
            color="primary"
            nuxt
            to="/users"
          >
            Registro
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>

export default {

}
</script>
