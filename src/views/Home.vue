<template>
  <v-app
    id="inspire"
    class="input"
  >
    <v-container fluid>
      <!-- FRONT PAGE TEXT -->
      <v-layout
        row
        wrap
      >
        <v-flex xs12>
          <v-img
            :src="frontImage"
            height="60vh"
          >
            <div class="homeText">
              <h1 class="homeText__main">Najboljše ponudbe za najem vozil na enem mestu!</h1>
              <h4 class="homeText__sub">Primerjaj najboljše ponudbe po najboljših cenah</h4>
            </div>
          </v-img>
        </v-flex>
      </v-layout>

      <!-- INPUT FORM  -->
      <!-- class input row is used to set Form in right position -->
      <div class="inputRow">
        <v-layout
          row
          wrap
        >
          <v-flex
            xs12
            md6
            pa-2
          >
            <v-card color="#33a8d5">
              <v-card-text>

                <v-form
                  ref="form"
                  v-model="valid"
                  lazy-validation
                >
                  <v-autocomplete
                    v-model="SearchedLocation"
                    :items="items"
                    :loading="isLoading"
                    :search-input.sync="search"
                    class="pickupLocation"
                    hide-no-data
                    item-text="name"
                    item-value="API"
                    placeholder="Lokacija prevzema"
                    prepend-icon="mdi-map-marker"
                    return-object
                    :rules="nameRules"
                    required
                  ></v-autocomplete>

                  <!-- Selection area date / time pickers -->
                  <v-container
                    grid-list-md
                    class="SelectionConteiner"
                  >
                    <v-layout
                      row
                      wrap
                    >
                      <v-flex lg6>
                        <!-- DATE SELECTION AREA -->

                        <div class="datetimePickupArea">
                          <v-menu
                            class="menuDatePickup"
                            v-model="menuDatePickup"
                            :close-on-content-click="false"
                            :nudge-right="40"
                            lazy
                            transition="scale-transition"
                            offset-y
                            full-width
                            min-width="290px"
                          >
                            <template v-slot:activator="{ on }">
                              <v-text-field
                                v-model="PickupDate"
                                label="Datum prevzema avtomobila"
                                prepend-icon="mdi-calendar"
                                readonly
                                v-on="on"
                              ></v-text-field>
                            </template>
                            <v-date-picker
                              v-model="PickupDate"
                              @input="menuDatePickup = false"
                            ></v-date-picker>
                          </v-menu>

                          <!-- TIME SELECT popup -->
                          <v-menu
                            class="menuTimePickup"
                            ref="menuTimePickup"
                            v-model="menuTimePickup"
                            :close-on-content-click="false"
                            :nudge-right="40"
                            :return-value.sync="timePickup"
                            lazy
                            transition="scale-transition"
                            offset-y
                            full-width
                            max-width="290px"
                            min-width="290px"
                          >
                            <template v-slot:activator="{ on }">
                              <v-text-field
                                v-model="timePickup"
                                prepend-icon="mdi-clock"
                                readonly
                                v-on="on"
                              ></v-text-field>
                            </template>
                            <v-time-picker
                              :allowed-minutes="allowedStep"
                              class="mt-3"
                              format="24hr"
                              v-if="menuTimePickup"
                              v-model="timePickup"
                              full-width
                              @click:minute="$refs.menuTimePickup.save(timePickup)"
                            ></v-time-picker>
                          </v-menu>
                        </div>
                      </v-flex>

                      <!-- DATE / TIME RETURN SELECTION AREA -->

                      <v-flex lg6>
                        <v-menu
                          class="menuDateReturn"
                          v-model="menuDateReturn"
                          :close-on-content-click="false"
                          :nudge-right="40"
                          lazy
                          transition="scale-transition"
                          offset-y
                          full-width
                          min-width="290px"
                          min="timePickup"
                        >
                          <template v-slot:activator="{ on }">
                            <v-text-field
                              v-model="ReturnDate"
                              label="Datum vračila avtomobila"
                              prepend-icon="mdi-calendar"
                              readonly
                              v-on="on"
                            ></v-text-field>
                          </template>
                          <v-date-picker
                            v-model="ReturnDate"
                            @input="menuDateReturn = false"
                          ></v-date-picker>
                        </v-menu>
                        <!-- Time picker -> return the car -->

                        <v-menu
                          ref="menuTimeReturn"
                          v-model="menuTimeReturn"
                          :close-on-content-click="false"
                          :nudge-right="40"
                          :return-value.sync="timeReturn"
                          lazy
                          transition="scale-transition"
                          offset-y
                          full-width
                          max-width="290px"
                          min-width="290px"
                        >
                          <template v-slot:activator="{ on }">
                            <v-text-field
                              v-model="timeReturn"
                              prepend-icon="mdi-clock"
                              readonly
                              v-on="on"
                            ></v-text-field>
                          </template>

                          <v-time-picker
                            v-model="timeReturn"
                            :allowed-minutes="allowedStep"
                            class="mt-3"
                            format="24hr"
                            v-if="menuTimeReturn"
                            full-width
                            @click:minute="$refs.menuTimeReturn.save(timeReturn)"
                          ></v-time-picker>
                        </v-menu>
                      </v-flex>
                    </v-layout>
                  </v-container>

                  <!-- select country of origin and drivers age -->

                  <v-container
                    class="SelectionConteiner"
                    grid-list-md
                  >
                    <v-layout>
                      <v-flex lg6>
                        <v-flex xs12>
                          <v-autocomplete
                            v-model="SearchedCountryOfOrigin"
                            :items="ApiOriginStates"
                            :label="`Vaša država:`"
                            :search-input.sync="searchOrigin"
                            :loading="isLoadingOrigin"
                            persistent-hint
                            prepend-icon="mdi-city"
                            item-text="name"
                            class="OriginLocation"
                            hide-no-data
                            return-object
                            item-value="API"
                            :rules="nameRules"
                          >
                          </v-autocomplete>
                        </v-flex>
                      </v-flex>
                      <v-flex lg6>
                        <v-checkbox
                          v-model="CheckDriversAge"
                          label="Sem voznik star med 30 in 65."
                        ></v-checkbox>
                      </v-flex>
                    </v-layout>
                  </v-container>

                  <!-- search button area -->

                  <v-layout row>
                    <v-flex
                      xs12
                      sm6
                      offset-sm3
                    >
                      <router-link :to="{path: 'search',
                        query: {
                          PickUpLocationId: this.SearchedLocation.id,
                          DropOffLocationId:this.SearchedLocation.id,
                          PickTime: this.PickupDate,
                          DropTime: this.ReturnDate,
                          DrvAge : this.DriversAge,
                          DrvCountry : this.SearchedCountryOfOrigin.id,
                          currency: this.SearchedLocation.id }}">
                        <v-btn
                          class="primary"
                          type="submit"
                          @click="onCreateSearch"
                        >IŠČI</v-btn>
                      </router-link>
                    </v-flex>
                  </v-layout>
                </v-form>
              </v-card-text>
            </v-card>
          </v-flex>

          <!-- description area -->

          <v-flex
            pa-5
            xs12
            md6
            class="text-xs-left inputRowInfo"
          >
            <h3>Rezervirajte enostavno in brez stresa:</h3>
            <v-layout
              row
              wrap
            >
              <v-flex
                xs3
                md12
                ma-2
              >
                <p>
                  <v-icon
                    size="30"
                    color="#33a8d5"
                  >mdi-checkbox-marked-circle-outline</v-icon>Brez stroškov odpovedi rezervacije
                </p>
              </v-flex>
              <v-flex
                xs3
                md12
                ma-2
              >
                <p>
                  <v-icon
                    size="30"
                    color="#33a8d5"
                  >mdi-checkbox-marked-circle-outline</v-icon>Brez skritih stroškov
                </p>
              </v-flex>
              <v-flex
                xs3
                md12
                ma-2
              >
                <p>
                  <v-icon
                    size="30"
                    color="#33a8d5"
                  >mdi-checkbox-marked-circle-outline</v-icon>Skrbimo za svoje stranke
                </p>
              </v-flex>
            </v-layout>
          </v-flex>
        </v-layout>
      </div>
    </v-container>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    // hero image
    frontImage: require('../img/home.jpg'),

    // list of locations from API
    entries: [],
    OriginEntries: [],
    valid: false,
    // show loader when loading from API
    isLoading: false,
    isLoadingOrigin: false,
    // Selected pick up location
    SearchedLocation: '',
    // Check if inputs are not empty
    nameRules: [
      (v) => !!v || 'To polje je obvezno'
    ],

    search: null,
    searchOrigin: null,

    PickupDate: new Date().toISOString().substr(0, 10),
    ReturnDate: new Date().toISOString().substr(0, 10),

    // All pick menues are closed when page loads
    menuDatePickup: false,
    menuDateReturn: false,
    menuTimePickup: false,
    menuTimeReturn: false,

    // default times
    timePickup: '12:00',
    timeReturn: '12:00',

    // check box for drivers age
    CheckDriversAge: true,
    // default drivers age

    DriversAge: 30,
    //  default country of origin
    SearchedCountryOfOrigin: '',
    isSubmitted: false
  }),
  computed: {

    items () {
      return this.entries.map(entry => {
        const name = entry.name
        return Object.assign({}, entry, { name })
      })
    },
    ApiOriginStates () {
      return this.OriginEntries.map(entry => {
        const name = entry.name
        return Object.assign({}, entry, { name })
      })
    }
  },
  watch: {
    search (val) {
      // Items have already been loaded
      if (this.items.length > 0) return
      // Items have already been requested
      if (this.isLoading) return
      this.isLoading = true
      // fetch all the locations from API
      fetch('http://www.mocky.io/v2/5c372b6e3000006e001f6297')
        .then(res => res.json())
        .then(res => {
          // console.log(JSON.stringify(res));
          const { response } = res
          const entries = response.data.locations
          console.log(entries)
          this.entries = entries
        })
        .catch(err => {
          console.log(err)
        })
        .finally(() => (this.isLoading = false))
    },
    searchOrigin (val) {
      // Items have already been loaded
      if (this.ApiOriginStates.length > 0) return
      // Items have already been requested
      if (this.isLoadingOrigin) return
      this.isLoadingOrigin = true
      // fetch all the locations from API
      fetch('http://www.mocky.io/v2/5cf58b5f2f0000ad7a4f08c6')
        .then(res => res.json())
        .then(res => {
          // console.log(JSON.stringify(res));
          const { response } = res
          const OriginEntries = response.data.residenceCountries
          // console.log(OriginEntries)
          this.OriginEntries = OriginEntries
        })
        .catch(err => {
          console.log(err)
        })
        .finally(() => (this.isLoadingOrigin = false))
    }
  },
  methods: {
    validate () {
      if (this.$refs.form.validate()) {
        this.snackbar = true
      }
    },
    // on submit create const with search creteria
    onCreateSearch () {
      this.$refs.form.validate()
    },
    submitted () {
      this.isSubmitted = true
    },
    // set interval for time picking - > minutes
    allowedStep: m => m % 15 === 0
  },

  // If all filter criteria are valid, create Search object and move to result page
  beforeRouteLeave (to, from, next) {
    if (this.valid) {
      const SearchedData = {
        SearchedLocationID: this.SearchedLocation.id,
        SearchedLocationName: this.SearchedLocation.name,
        PickupDate: this.PickupDate,
        ReturnDate: this.ReturnDate,
        CountryOfOrigin: this.SearchedCountryOfOrigin.id,
        DriversAge: this.DriversAge
      }
      console.log(SearchedData)
      next()
    } else {
      next(false)
    }
  }
}
</script>

<style lang="scss" scoped>
@mixin respond($breakpoint) {
  @if $breakpoint == tab-port {
    @media only screen and (max-width: 56.25em) {
      @content;
    }
  }
}
// set site of home image
.homeImg {
  width: 100%;
  height: 30rem;
}
// move input to right position
.inputRow {
  margin-top: -10rem;
}
// move info text to right position
.inputRowInfo {
  margin-top: 10rem;
  @include respond(tab-port) {
    margin-top: 0rem;
  }
}
// set padding for all elements in input field
.SelectionConteiner {
  padding: 0px 1px 0px 1px;
}
// position of home text
.homeText {
  position: absolute;
  padding: 2rem;
  //max-width:30rem;
  color: white;
  text-align: left;
  &__main {
    font-weight: 800;
    margin-bottom: 2rem;
  }
  &__sub {
    font-weight: 100;
  }
}
.OriginLocation {
  background-color: #33a8d5;
}

.inputField {
  position: absolute;
  top: 20rem;
  left: 10rem;
  height: 30rem;
  width: 50rem;
  background-color: #33a8d5;
}
.pickupLocation {
  padding: 1rem 1rem 0rem 1rem;
  background-color: rgb(255, 255, 255);
  margin-bottom: 2rem;
}
.menuDatePickup {
  padding: 0px;
}
.datetime {
  position: relative;
  width: 100%;
  &__pickup {
    position: absolute;
    left: 0;
    // background-color: green;
    width: 50%;
    &__date {
      width: 50%;
    }
    &__time {
      width: 50%;
    }
  }
  &__return {
    position: absolute;
    left: 50%;
    // background-color: red;
    width: 50%;
  }
}
</style>
