<template>
  <v-layout row wrap>
    <v-flex xs6 sm8>
      <v-card>
        <v-card-actions>
          <v-form ref="form" v-model="valid" lazy-validation>
            <v-container>
              <v-row>
                <v-col
                  cols="8"
                  md="6"
                >
                  <v-text-field
                    v-model="name"
                    :rules="nameRules"
                    :counter="10"
                    label="Nombre y apellidos"
                    required
                  />
                </v-col>

                <v-col
                  cols="8"
                  md="6"
                >
                  <v-text-field
                    v-model="namereport"
                    :rules="nameRules"
                    :counter="10"
                    label="Nombre de quien reporta"
                  />
                </v-col>
              </v-row>
              <v-row>
                <v-col
                  cols="16"
                  md="6"
                >
                  <v-menu
                    ref="menu"
                    v-model="menu"
                    :close-on-content-click="false"
                    :nudge-right="40"
                    :return-value.sync="date"
                    transition="scale-transition"
                    offset-y
                    min-width="290px"
                  >
                    <template v-slot:activator="{ on }">
                      <v-text-field
                        v-model="date1"
                        v-on="on"
                        label="Fecha de nacimiento"
                        prepend-icon="event"
                        readonly
                      />
                    </template>
                    <v-date-picker v-model="date1" no-title scrollable>
                      <v-spacer />
                      <v-btn @click="menu = false" flat color="primary">
                        Cancelar
                      </v-btn>
                      <v-btn @click="$refs.menu.save(date1)" flat color="primary">
                        OK
                      </v-btn>
                    </v-date-picker>
                  </v-menu>
                </v-col>

                <v-spacer />
                <v-col
                  cols="16"
                  md="6"
                >
                  <v-text-field
                    v-model="namebirthplace"
                    :rules="nameRules"
                    :counter="10"
                    label="Lugar de nacimiento"
                  />
                </v-col>
              </v-row>
              <v-row>
                <v-col
                  cols="16"
                  md="6"
                >
                  <v-menu
                    ref="menu"
                    v-model="menu2"
                    :close-on-content-click="false"
                    :nudge-right="40"
                    :return-value.sync="date"
                    transition="scale-transition"
                    offset-y
                    min-width="290px"
                  >
                    <template v-slot:activator="{ on }">
                      <v-text-field
                        v-model="date2"
                        v-on="on"
                        label="Fecha de desaparición"
                        prepend-icon="event"
                        readonly
                      />
                    </template>
                    <v-date-picker v-model="date2" no-title scrollable>
                      <v-spacer />
                      <v-btn @click="menu2 = false" flat color="primary">
                        Cancelar
                      </v-btn>
                      <v-btn @click="$refs.menu2.save(date2)" flat color="primary">
                        OK
                      </v-btn>
                    </v-date-picker>
                  </v-menu>
                </v-col>
                <v-spacer />
                <v-col
                  class="d-flex"
                  cols="16"
                  sm="6"
                >
                  <v-select
                    :items="items"
                    label="Sexo"
                  />
                </v-col>
              </v-row>
              <v-row>
                <v-col
                  cols="16"
                  sm="6"
                >
                  <v-text-field
                    v-model="streetname"
                    :rules="nameRules"
                    :counter="10"
                    label="Calle"
                  />
                </v-col>
                <v-col
                  cols="16"
                  sm="6"
                >
                  <v-text-field
                    v-model="cityname"
                    :rules="nameRules"
                    :counter="10"
                    label="Ciudad"
                  />
                </v-col>
              </v-row>
              <v-row>
                <v-spacer />
                <v-btn
                  :disabled="!valid"
                  @click="register()"
                  color="primary"
                >
                  Registrar
                </v-btn>
              </v-row>
            </v-container>
          </v-form>
        </v-card-actions>
        <v-dialog v-model="dialog" persistent max-width="320">
          <v-card>
            <v-card-title class="headline">
              Advertencia!
            </v-card-title>
            <v-card-text>Are you sure you want to delete this user</v-card-text>
            <v-card-actions>
              <v-spacer />
              <v-btn @click="hideDialog()" color="green darken-1" flat>
                Cancelar.
              </v-btn>
              <v-btn @click="deleteUpload()" color="green darken-1" flat>
                Si.
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
export default {
  data () {
    return {
      dialog: false,
      selectedUser: null,
      valid: true,
      name: null,
      nameRules: [
        v => !!v || 'Se requiere el nombre completo',
        v => (v && v.length > 2) || 'Debe contener mas de dos caracteres'
      ],
      items: ['F', 'M'],
      date: new Date().toISOString().substr(0, 10),
      date2: new Date().toISOString().substr(0, 10),
      menu: false,
      modal: false,
      menu2: false
    }
  },

  computed: {
    users () {
      return this.$store.state.user.list
    }
  },
  fetch ({ store }) {
    return store.dispatch('user/getAll')
  },

  methods: {
    register () {
      const self = this
      if (this.$refs.form.validate()) {
        return this.$store.dispatch('user/register', this.name)
          .then(() => {
            return self.$router.push({ path: `/users/${self.name}` })
          })
      }
    },

    showDialog (name) {
      this.dialog = true
      this.selectedUser = name
    },

    hideDialog () {
      this.dialog = false
      this.selectedUser = null
    },

    async deleteUpload () {
      if (this.selectedUser) {
        await this.$store.dispatch('user/delete', this.selectedUser)
        this.selectedUser = null
        this.dialog = false
      }
    }
  }
}
</script>
