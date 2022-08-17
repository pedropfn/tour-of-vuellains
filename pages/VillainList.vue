<template>
  <v-card elevation="2">
    <v-card-title>Villains List</v-card-title>
    <v-card-subtitle>Select your villain</v-card-subtitle>
    <v-divider class="mx-4"></v-divider>
    <v-simple-table fixed-header>
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
              <v-btn icon color="success">
                <v-icon dark>mdi-pencil</v-icon>
              </v-btn>
            </td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
    <v-divider class="mx-4"></v-divider>
    <v-card-text>
      <pre>{{ message }}</pre>
    </v-card-text>
  </v-card>
</template>

<script>
const ourVillains = [
  {
    id: 10,
    firstName: 'Toya',
    lastName: 'Todoroki',
    description: 'Blue flame Dabi',
  },
  {
    id: 20,
    firstName: 'Chizome',
    lastName: 'Akaguro',
    description: 'Hero killer Stain',
  },
  {
    id: 30,
    firstName: 'Kai',
    lastName: 'Chisaki',
    description: 'Yakuza Leader Overhaul',
  },
  {
    id: 40,
    firstName: 'Jin',
    lastName: 'Bubaigawara',
    description: 'Twice',
  },
  {
    id: 50,
    firstName: 'Tomura',
    lastName: 'Shigaraki',
    description: 'Symbol of Fear',
  },
]

export default {
  name: 'IndexPage',
  data() {
    return {
      villains: [],
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
  },
}
</script>
