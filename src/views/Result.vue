<template>

  <!-- LOADER WHEN GETTING DATA FROM API -->

  <v-container
    bg
    fill-height
    v-if="loading"
  >
    <v-layout
      row
      wrap
      align-center
    >
      <v-flex>
        <v-progress-circular
          :size="70"
          :width="7"
          color="green"
          indeterminate
        ></v-progress-circular>
      </v-flex>
    </v-layout>
  </v-container>

  <v-container
    v-else
    grid-list-sm
  >
    <v-layout
      row
      wrap
    >

      <!-- FILTER AREA -->

      <v-flex
        xs12
        sm4
        md3
        lg2
      >
        <v-expansion-panel>
          <v-expansion-panel-content>
            <template v-slot:header>
              <div class="filterButtonText">Razvrsti po ceni</div>
            </template>
            <v-card>
              <v-card-text>
                <div class="sort-orders">
                  <v-btn
                    @click="sort('vehicle.smallSuitcases','asc')"
                    color="green"
                    >Cenejši naprej</v-btn>
                  <v-btn
                    @click="sort('vehicle.smallSuitcases','desc')"
                    color="red"
                  >Dražji naprej</v-btn>
                </div>
              </v-card-text>
            </v-card>
          </v-expansion-panel-content>
        </v-expansion-panel>
        <v-expansion-panel>
          <v-expansion-panel-content>
            <template v-slot:header>
              <div class="filterButtonText">Lokacije prevzema</div>
            </template>
            <v-card>
              <v-card-text>
                <v-checkbox
                  v-model="checkedLocations"
                  :label="`Terminal`"
                  value="Terminal"
                ></v-checkbox>
                <v-checkbox
                  v-model="checkedLocations"
                  :label="`Airport`"
                  value="Airport"
                ></v-checkbox>
              </v-card-text>
            </v-card>
          </v-expansion-panel-content>
        </v-expansion-panel>
        <v-expansion-panel>
          <v-expansion-panel-content>
            <template v-slot:header>
              <div class="filterButtonText">Skupine avtomobilov</div>
            </template>
            <v-card>
              <v-card-text>
                <v-checkbox v-model="FilterCheckboxSmallCar">
                  <template v-slot:label>
                    <v-icon
                      size="20"
                      color="grey"
                    >mdi-car</v-icon>
                    <div>Majhen avtomobil</div>
                  </template>
                </v-checkbox>
                <v-checkbox
                  v-model="FilterCheckboxMiddleCar"
                  :label="`Srednje velik avtomobil`"
                >
                  <template v-slot:label>
                    <v-icon
                      size="25"
                      color="grey"
                    >mdi-car</v-icon>
                    <div>Srednje velik avtomobil</div>
                  </template>
                </v-checkbox>
                <v-checkbox
                  v-model="FilterCheckboxBigCar"
                  :label="`Velik avtomobil`"
                >
                  <template v-slot:label>
                    <v-icon
                      size="30"
                      color="grey"
                    >mdi-car</v-icon>
                    <div>Velik avtomobil</div>
                  </template>
                </v-checkbox>
                <v-checkbox
                  v-model="FilterCheckboxLongCar"
                  :label="`Karavan`"
                >
                  <template v-slot:label>
                    <v-icon
                      size="30"
                      color="grey"
                    >mdi-van-passenger</v-icon>
                    <div>Karavan</div>
                  </template>
                </v-checkbox>
                <v-checkbox
                  v-model="FilterCheckboxPremiumCar"
                  :label="`Premium avtomobil`"
                >
                  <template v-slot:label>
                    <v-icon color="grey">mdi-bus</v-icon>
                    <div>Premium avtomobil</div>
                  </template>
                </v-checkbox>
                <v-checkbox
                  v-model="FilterCheckboxVan"
                  :label="`Kombi`"
                >
                  <template v-slot:label>
                    <v-icon color="grey">mdi-van-passenger</v-icon>
                    <div>Kombi</div>
                  </template>
                </v-checkbox>
                <v-checkbox
                  v-model="FilterCheckboxSUV"
                  :label="`SUV`"
                >
                  <template v-slot:label>
                    <v-icon
                      size="30"
                      color="grey"
                    >mdi-van-utility</v-icon>
                    <div>SUV</div>
                  </template>
                </v-checkbox>
              </v-card-text>
            </v-card>
          </v-expansion-panel-content>
        </v-expansion-panel>
        <v-expansion-panel>
          <v-expansion-panel-content>
            <template v-slot:header>
              <div class="filterButtonText">Cena</div>
            </template>
          </v-expansion-panel-content>
        </v-expansion-panel>
      </v-flex>

      <!-- RESULT AREA -->

      <v-flex
        xs12
        sm8
        md9
        lg10
      >

        <v-flex xs12>
          <h3 v-if='filteredPickupLocation.length === 0'>Žal ni ponudb, ki bi ustrezale izbranim pogojem.</h3>
        </v-flex>

        <div
          name="fade-list"
          is="transition-group"
        >

          <v-flex
            xs12
            mb-4
            v-for="offer in filteredPickupLocation"
            :key="offer.id"
            class="offerena"
          >

            <offer-app :offer="offer" ></offer-app>

          </v-flex>
        </div>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import axios from 'axios'
import _ from 'lodash'

import offer from '../components/offer.vue'

export default {
  data () {
    return {
      // list of all offers from API
      offers: [],
      // popup activator for detailed offer view
      loading: true,

      // data for filter
      FilterCheckboxSmallCar: '',
      FilterCheckboxMiddleCar: '',
      FilterCheckboxBigCar: '',
      FilterCheckboxLongCar: '',
      FilterCheckboxPremiumCar: '',
      FilterCheckboxVan: '',
      FilterCheckboxSUV: '',

      checkedLocations: [],

      orderBy: 'position',
      orderOption: 'asc'
    }
  },

  created () {
    // get data from api
    // i used external library axios
    axios
      .get('http://www.mocky.io/v2/5c3733a630000090001f62de?mocky-delay=5000ms')
      .then(response => {
        const offers = response.data.response.data.offers.offers
        this.offers = offers
        this.loading = false
        console.log(this.offers)
      })
      .catch(e => {
        console.error(e)
      })
  },

  methods: {
    // sorting method
    sort: function (by, option) {
      if (this.orderBy === by) {
        if (this.orderOption === 'asc') {
          this.orderOption = 'desc'
        } else if (this.orderOption === 'desc') {
          this.orderOption = 'asc'
        }
      } else {
        this.orderOption = option
        this.orderBy = by
      }
    }
  },

  computed: {
    // filtering function - if no pickup location isn's picked - show all
    filteredPickupLocation () {
      if (!this.checkedLocations.length) { return this.sortedOffers }
      return this.sortedOffers.filter(offer => this.checkedLocations.includes(offer.pickupBranch.type.name))
    },
    // create sorted offers by criteria
    sortedOffers: function () {
      return _.orderBy(this.offers, this.orderBy, this.orderOption)
    }
  },
  // imported components
  components: {
    offerApp: offer
  }
}
</script>

<style lang="scss" scoped>

.v-expansion-panel {
  // max-width: 250px;
  -webkit-border-radius: 4px;
  -moz-border-radius: 4px;
  border-radius: 4px;
}

.filterFlex {
  min-width: 300px;
}
.BoxSubtitle {
  color: rgb(111, 180, 111);
}

ul {
  list-style-type: none;
}
.offerena {
  border: 1px solid rgb(180, 178, 178);
}

.offerena:hover {
  border: 1px solid rgb(128, 128, 128);
}

.filterButtonText {
  color: #8f8f8f;
  font-weight: 700;
  font-size: 1.1em;
}

// list transition
.fade-list-move {
  transition: transform 0.35s ease;
}

.fade-list-leave-to {
  transition: all 0.5s ease;
  opacity: 0;
}
</style>
