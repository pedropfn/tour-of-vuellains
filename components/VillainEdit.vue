<template>
  <v-container elevation="2">
    <v-card-title>Vuellain</v-card-title>
    <v-card-subtitle>{{ fullName }}</v-card-subtitle>
    <v-card-text>
      <v-form>
        <v-container>
          <v-row>
            <v-col cols="5" class="mx-10">
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
                <v-text-field
                  id="crimeCounter"
                  v-model="villain.crimeCounter"
                  label="Crime Counter"
                ></v-text-field>
              </v-row>
              <v-row>
                <v-text-field
                  id="crimeRank"
                  v-model="villain.crimeRank"
                  label="Villain Rank"
                  readonly
                ></v-text-field>
              </v-row>
            </v-col>
            <v-col cols="5" class="mx-10">
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
                <v-radio-group
                  v-model="villain.capeColor"
                  label="Cape Color"
                  row
                >
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
                <v-checkbox
                  id="active"
                  v-model="villain.active"
                  color="success"
                  label="Active"
                />
              </v-row>
              <v-row>
                <v-card-text> Villain since {{ formattedDate }} </v-card-text>
              </v-row>
              <v-row>
                <v-menu
                  ref="menu"
                  v-model="menu"
                  :close-on-content-click="false"
                  :return-value.sync="villain.originDate"
                  transition="scale-transition"
                  offset-y
                  min-width="auto"
                >
                  <template #activator="{ on, attrs }">
                    <v-text-field
                      v-model="formattedDate"
                      label="Origin Date"
                      prepend-icon="mdi-calendar"
                      readonly
                      v-bind="attrs"
                      v-on="on"
                    ></v-text-field>
                  </template>
                  <v-date-picker
                    id="originDate"
                    v-model="villain.originDate"
                    no-title
                    scrollable
                  >
                    <v-spacer></v-spacer>
                    <v-btn text color="success" @click="menu = false">
                      Cancel
                    </v-btn>
                    <v-btn
                      text
                      color="success"
                      @click="$refs.menu.save(villain.originDate)"
                    >
                      OK
                    </v-btn>
                  </v-date-picker>
                </v-menu>
              </v-row>
            </v-col>
          </v-row>
        </v-container>
      </v-form>
    </v-card-text>
    <v-container>
      <v-card-actions>
        <v-btn color="error" tile @click="cancelVillain()">
          <v-icon dark>mdi-close</v-icon>
          Cancel
        </v-btn>
        <v-btn color="success" tile @click="saveVillain()">
          <v-icon dark>mdi-pencil</v-icon>
          Save
        </v-btn>
      </v-card-actions>
    </v-container>
  </v-container>
</template>

<script>
import { format, parseISO } from 'date-fns'

const displayDateFormat = 'MM/dd/yyyy'

export default {
  name: 'VillainEdit',
  props: {
    editVillain: {
      type: Object,
      default: () => {},
    },
  },
  data() {
    return {
      villain: { ...this.editVillain },
      powers: ['Speed', 'Flight', 'Strength', 'Invisibility', 'Fire'],
      message: '',
      menu: false,
    }
  },
  computed: {
    fullName() {
      return `${this.villain.firstName} ${this.villain.lastName}`
    },
    formattedDate() {
      return format(parseISO(this.villain.originDate), displayDateFormat)
    },
  },
  watch: {
    'villain.crimeCounter': {
      immediate: true,
      handler(newRank) {
        this.handleCrimes(newRank)
      },
    },
  },
  methods: {
    cancelVillain() {
      this.$emit('cancel')
    },
    saveVillain() {
      this.$emit('save', this.editVillain)
    },
    clearPower() {
      this.villain.power = ''
    },
    handleCrimes(newRank) {
      const rank = parseInt(newRank, 10)
      switch (rank) {
        case 0:
          this.villain.crimeRank = 'C rank Villain'
          break
        case 1:
          this.villain.crimeRank = 'B rank Villain'
          break
        case 2:
          this.villain.crimeRank = 'A rank Villain'
          break
        default:
          this.villain.crimeRank = 'S rank Villain'
          break
      }
    },
  },
}
</script>
