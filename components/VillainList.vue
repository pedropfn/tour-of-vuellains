<template>
  <v-card elevation="2">
    <v-card-title>Welcome to Tour of Vuellains</v-card-title>
    <v-card-subtitle>Select a villain for more details</v-card-subtitle>
    <VillainEdit
      v-if="selectedVillain"
      :edit-villain="selectedVillain"
      @save="saveVillain"
      @cancel="cancelVillain"
    />
    <v-simple-table v-if="!selectedVillain" fixed-header>
      <template #default>
        <thead>
          <tr>
            <th class="text-left">Name</th>
            <th class="text-left">Description</th>
            <th class="text-right"></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="villain in villains" :key="villain.id">
            <td>{{ villain.firstName }}</td>
            <td>{{ villain.description }}</td>
            <td>
              <v-btn icon color="success" @click="selectVillain(villain)">
                <v-icon dark>mdi-pencil</v-icon>
              </v-btn>
            </td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
    <v-card-text>
      <pre>{{ message }}</pre>
    </v-card-text>
  </v-card>
</template>

<script>
import { format, parseISO } from 'date-fns'
import VillainEdit from './VillainEdit.vue'

const inputDateFormat = 'yyyy-MM-dd'

const ourVillains = [
  {
    id: 10,
    firstName: 'Toya',
    lastName: 'Todoroki',
    description: 'Blue flame Dabi',
    capeColor: 'blue',
    power: '',
    active: true,
    crimeCounter: 4,
    crimeRank: '',
    originDate: format(
      parseISO(new Date(1996, 5, 1).toISOString()),
      inputDateFormat
    ),
  },
  {
    id: 20,
    firstName: 'Chizome',
    lastName: 'Akaguro',
    description: 'Hero killer Stain',
    capeColor: 'red',
    power: '',
    active: false,
    crimeCounter: 4,
    crimeRank: '',
    originDate: format(
      parseISO(new Date(1996, 5, 1).toISOString()),
      inputDateFormat
    ),
  },
  {
    id: 30,
    firstName: 'Kai',
    lastName: 'Chisaki',
    description: 'Yakuza Leader Overhaul',
    capeColor: 'green',
    power: '',
    active: false,
    crimeCounter: 4,
    crimeRank: '',
    originDate: format(
      parseISO(new Date(1996, 5, 1).toISOString()),
      inputDateFormat
    ),
  },
  {
    id: 40,
    firstName: 'Jin',
    lastName: 'Bubaigawara',
    description: 'Twice',
    capeColor: 'red',
    power: '',
    active: true,
    crimeCounter: 4,
    crimeRank: '',
    originDate: format(
      parseISO(new Date(1996, 5, 1).toISOString()),
      inputDateFormat
    ),
  },
  {
    id: 50,
    firstName: 'Tomura',
    lastName: 'Shigaraki',
    description: 'Symbol of Fear',
    capeColor: 'blue',
    power: '',
    active: true,
    crimeCounter: 4,
    crimeRank: '',
    originDate: format(
      parseISO(new Date(1996, 5, 1).toISOString()),
      inputDateFormat
    ),
  },
]

export default {
  name: 'IndexPage',
  components: { VillainEdit },
  data() {
    return {
      villains: [],
      selectedVillain: undefined,
      message: '',
    }
  },
  created() {
    this.loadVillains()
  },
  methods: {
    getVillains() {
      return new Promise((resolve) => {
        setTimeout(() => resolve(ourVillains), 1500)
      })
    },
    async loadVillains() {
      this.villains = []
      this.message = 'getting the Villains, please be patient'
      this.villains = await this.getVillains()
      this.message = ''
    },
    selectVillain(villain) {
      this.message = ''
      this.selectedVillain = villain
    },
    cancelVillain() {
      this.message = ''
      this.selectedVillain = undefined
    },
    saveVillain() {
      this.message = JSON.stringify(this.selectedVillain, null, '\n ')
      this.selectedVillain = undefined
    },
  },
}
</script>
