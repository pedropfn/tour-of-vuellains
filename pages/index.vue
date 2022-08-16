<template>
  <v-card elevation="2">
    <v-card-title>Vuellain</v-card-title>
    <v-card-subtitle>{{ villain.firstName }}</v-card-subtitle>
    <v-card-text>
      <v-form>
        <v-container>
          <v-row>
            <v-text-field
              id="id"
              v-model="villain.id"
              label="Id"
              readonly
            ></v-text-field>
          </v-row>
          <v-row>
            <v-text-field
              id="firstName"
              v-model="villain.firstName"
              label="First Name"
            />
          </v-row>
          <v-row>
            <v-text-field
              id="lastName"
              v-model="villain.lastName"
              label="Last Name"
            />
          </v-row>
          <v-row>
            <v-textarea
              id="description"
              v-model="villain.description"
              rows="2"
              label="Description"
            />
          </v-row>
          <v-row>
            <v-radio-group v-model="villain.capeColor" label="Cape Color" row>
              <v-radio
                id="color-red"
                value="red"
                label="Red"
                color="red"
              ></v-radio>
              <v-radio
                id="color-blue"
                value="blue"
                label="Blue"
                color="blue"
              ></v-radio>
              <v-radio
                id="color-green"
                value="green"
                label="Green"
                color="green"
              ></v-radio>
            </v-radio-group>
          </v-row>
          <v-row>
            <v-select
              id="power"
              v-model="villain.power"
              :items="powers"
              label="Super Power"
              hint="Please select one"
              @keyup.esc="clearPower"
            >
            </v-select>
          </v-row>
          <v-row>
            <v-checkbox id="active" v-model="villain.active" label="Active" />
          </v-row>
        </v-container>
      </v-form>
    </v-card-text>
    <v-divider class="mx-4"></v-divider>
    <v-container>
      <v-card-actions>
        <v-btn @click="cancelvillain()">
          <span>Cancel</span>
        </v-btn>
        <v-btn @click="savevillain()">
          <span>Save</span>
        </v-btn>
      </v-card-actions>
    </v-container>
    <v-divider class="mx-4"></v-divider>
    <v-card-text class="notification is-info">
      <pre>{{ message }}</pre>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      villain: {
        id: 20,
        firstName: 'Toya',
        lastName: 'Todoroki',
        description: 'Fogo azul',
        capeColor: 'blue',
        power: '',
        active: true,
      },
      powers: ['Speed', 'Flight', 'Strength', 'Invisibility', 'Fire', ''],
      message: '',
    }
  },
  methods: {
    cancelvillain() {
      this.message = ''
    },
    clearPower() {
      this.villain.power = ''
    },
    savevillain() {
      // This only updates when you click the save button
      this.message = JSON.stringify(this.villain, null, '\n ')
    },
  },
}
</script>
