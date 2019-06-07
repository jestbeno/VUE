<template>
  <v-layout
    row
    mt-3
  >
    <v-flex class="offerDisplay1">
      <v-layout row>

        <!-- CAR IMAGE -->

        <v-flex xs5>
          <v-img
            :src="offer.vehicle.example.imageURL"
            height="125px"
            contain
          ></v-img>
        </v-flex>

        <!-- LOGO PONUDNIKA - INFO - AIRPORT/TERMINAL -->

        <v-flex
          xs7
          class="text-xs-left CardInfoLink"
        >
          <v-img
            position="left"
            :src="offer.pickupBranch.vendor.logoURL"
            height="25px"
            contain
          ></v-img>
          <p>
            <v-icon color="#33a8d5">mdi-information</v-icon>
            <a>Pomembne informacije</a>
          </p>
          <v-dialog
            v-model="dialog"
            width="600px"
            data-app
          >
            <template v-slot:activator="{ on }">
              <p>
                <v-icon color="#33a8d5">mdi-map-marker</v-icon>
                <a
                  color="#33a8d5"
                  v-on="on"
                >{{ offer.pickupBranch.type.name }}</a>
              </p>
            </template>
            <v-card>
              <v-card-title>
                <span class="headline">Prevzem</span>
              </v-card-title>
              <v-card-text>Storitev omogoča: {{ offer.pickupBranch.name }}, {{ offer.pickupBranch.address }}</v-card-text>
              <v-card-text>{{ offer.pickupBranch.pickupInstructions }}</v-card-text>
              <v-card-text>{{ offer.pickupBranch.pickupInstructions }}</v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn
                  color="green darken-1"
                  flat="flat"
                  @click="dialog = false"
                >OK</v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>
        </v-flex>
      </v-layout>

      <!-- Vihecle name -->

      <v-layout row>
        <v-flex
          xs12
          class="text-xs-center title font-weight-bold"
        >{{ offer.vehicle.example.name }} ali podobno</v-flex>
      </v-layout>

      <v-layout row>
        <v-flex
          xs12
          class="text-xs-center font-weight-bold"
        >
          <p class="BoxSubtitle">takojšnja potrditev</p>
        </v-flex>
      </v-layout>

      <!-- Icons for car description -->

      <v-layout
        align-start
        justify-space-around
        row
      >
        <v-flex xs2>
          <v-card>
            <v-card-text
              color="grey lighten-2"
              class="px-0"
            >
              <v-layout row>
                <v-flex xs12>
                  <v-icon color="#33a8d5">mdi-glassdoor</v-icon>
                </v-flex>
              </v-layout>
              <v-layout row>
                <v-flex xs12>
                  <p class="ValueOnIcons">{{ offer.vehicle.seats }}</p>
                </v-flex>
              </v-layout>
            </v-card-text>
          </v-card>
        </v-flex>
        <v-flex xs2>
          <v-card>
            <v-card-text
              color="grey lighten-2"
              class="px-0"
            >
              <v-layout row>
                <v-flex xs12>
                  <v-icon color="#33a8d5">mdi-usb</v-icon>
                </v-flex>
              </v-layout>
              <v-layout row>
                <v-flex xs12>
                  <p class="ValueOnIcons">{{ offer.vehicle.transmissionDrive.id }}</p>
                </v-flex>
              </v-layout>
            </v-card-text>
          </v-card>
        </v-flex>
        <v-flex xs2>
          <v-card>
            <v-card-text
              color="grey lighten-2"
              class="px-0"
            >
              <v-layout row>
                <v-flex xs12>
                  <v-icon color="#33a8d5">mdi-snowflake</v-icon>
                </v-flex>
              </v-layout>
              <v-layout row>
                <v-flex xs12>
                  <p class="ValueOnIcons">Da</p>
                </v-flex>
              </v-layout>
            </v-card-text>
          </v-card>
        </v-flex>
        <v-flex xs2>
          <v-card>
            <v-card-text
              color="grey lighten-2"
              class="px-0"
            >
              <v-layout row>
                <v-flex xs12>
                  <v-icon color="#33a8d5">mdi-human</v-icon>
                </v-flex>
              </v-layout>
              <v-layout row>
                <v-flex xs12>
                  <p class="ValueOnIcons">{{ offer.vehicle.seats }}</p>
                </v-flex>
              </v-layout>
            </v-card-text>
          </v-card>
        </v-flex>
        <v-flex xs2>
          <v-card>
            <v-card-text
              color="grey lighten-2"
              class="px-0"
            >
              <v-layout row>
                <v-flex xs12>
                  <v-icon color="#33a8d5">mdi-bag-personal</v-icon>
                </v-flex>
              </v-layout>
              <v-layout row>
                <v-flex xs12>
                  <p class="ValueOnIcons">{{ offer.vehicle.smallSuitcases }}</p>
                </v-flex>
              </v-layout>
            </v-card-text>
          </v-card>
        </v-flex>
        <v-flex xs2>
          <v-card>
            <v-card-text
              color="grey lighten-2"
              class="px-0"
            >
              <v-layout row>
                <v-flex xs12>
                  <v-icon color="#33a8d5">mdi-bag-personal</v-icon>
                </v-flex>
              </v-layout>
              <v-layout row>
                <v-flex xs12>
                  <p class="ValueOnIcons">{{ offer.vehicle.smallSuitcases }}</p>
                </v-flex>
              </v-layout>
            </v-card-text>
          </v-card>
        </v-flex>
        <v-flex xs2>
          <v-card>
            <v-card-text
              color="grey lighten-2"
              class="px-0"
            >
              <v-layout row>
                <v-flex xs12>
                  <v-icon color="#33a8d5">mdi-gas-station</v-icon>
                </v-flex>
              </v-layout>
              <v-layout row>
                <v-flex xs12>
                  <div>
                    <v-tooltip bottom>
                      <template v-slot:activator="{ on }">
                        <v-icon
                          size="20"
                          color="gray"
                          v-on="on"
                        >mdi-information</v-icon>
                      </template>
                      <span>Polno za polno</span>
                    </v-tooltip>
                  </div>
                </v-flex>
              </v-layout>
            </v-card-text>
          </v-card>
        </v-flex>
      </v-layout>

      <!-- EXPANSION BUTTONS OFFER - SHOWED ONLY ON SMALLER SCREENS -->
      <v-layout
        align-start
        justify-space-around
        row
        mt-4
        class="OfferButtons"
      >
        <v-expansion-panel>
          <v-expansion-panel-content class="grey">
            <template v-slot:actions>
              <v-icon color="white">$vuetify.icons.expand</v-icon>
            </template>
            <template v-slot:header>
              <div class="expansionHeader">
                <p class="font-weight-bold">BUDGET</p>
                <p>od {{offer.vehicle.deposit.amount/750}}€ / dan</p>
              </div>
            </template>
            <v-layout>
              <v-flex xs12>
                <v-card>
                  <v-card-title primary-title>
                    <div class="text-xs-center">
                      <div class="headline">BUDGET</div>
                      <div>{{offer.vehicle.deposit.amount}}€</div>
                      <div>{{offer.vehicle.deposit.amount/150}}€/dan</div>
                    </div>
                  </v-card-title>
                  <v-card-text>
                    <ul>
                      <li>
                        <v-icon
                          height="5"
                          v-text="neomejenaKilometrina ? 'mdi-check-outline' : 'mdi-window-close'"
                        ></v-icon>Neomejena kilometrina
                      </li>
                      <li>
                        <v-icon
                          height="5"
                          v-text="PolniKasko ? 'mdi-check-outline' : 'mdi-window-close'"
                        ></v-icon>Polno kasko zavarovanje
                      </li>
                      <li>
                        <v-icon
                          height="5"
                          v-text="StealCoverage ? 'mdi-check-outline' : 'mdi-window-close'"
                        ></v-icon>Zaščita pred krajo
                      </li>
                      <li>
                        <v-icon
                          height="5"
                          v-text="SuperExvessRefund ? 'mdi-check-outline' : 'mdi-window-close'"
                        ></v-icon>Super Excess Refund
                      </li>
                      <li>
                        <v-icon
                          height="5"
                          v-text="CancelEsuranse ? 'mdi-check-outline' : 'mdi-window-close'"
                        ></v-icon>Zavarovanje odpovedi
                      </li>
                    </ul>
                  </v-card-text>
                </v-card>
              </v-flex>
            </v-layout>
          </v-expansion-panel-content>
        </v-expansion-panel>
        <v-expansion-panel>
          <v-expansion-panel-content class="green lighten-2">
            <template v-slot:actions>
              <v-icon color="white">$vuetify.icons.expand</v-icon>
            </template>
            <template v-slot:header>
              <div class="expansionHeader">
                <p class="font-weight-bold title">RELAX</p>
                <!-- <br> -->
                <p>od {{offer.vehicle.deposit.amount/150}}€ / dan</p>
              </div>
            </template>
            <v-layout>
              <v-flex xs12>
                <v-card>
                  <v-card-title primary-title>
                    <div class="text-xs-center">
                      <div class="headline">RELAX</div>
                      <div>{{offer.vehicle.deposit.amount}}€</div>
                      <div>{{offer.vehicle.deposit.amount/150}}€/dan</div>
                    </div>
                  </v-card-title>
                  <v-card-text>
                    <ul>
                      <li>
                        <v-icon
                          height="5"
                          v-text="neomejenaKilometrina ? 'mdi-check-outline' : 'mdi-window-close'"
                        ></v-icon>Neomejena kilometrina
                      </li>
                      <li>
                        <v-icon
                          height="5"
                          v-text="PolniKasko ? 'mdi-check-outline' : 'mdi-window-close'"
                        ></v-icon>Polno kasko zavarovanje
                      </li>
                      <li>
                        <v-icon
                          height="5"
                          v-text="StealCoverage ? 'mdi-check-outline' : 'mdi-window-close'"
                        ></v-icon>Zaščita pred krajo
                      </li>
                      <li>
                        <v-icon
                          height="5"
                          v-text="SuperExvessRefund ? 'mdi-check-outline' : 'mdi-window-close'"
                        ></v-icon>Super Excess Refund
                      </li>
                      <li>
                        <v-icon
                          height="5"
                          v-text="CancelEsuranse ? 'mdi-check-outline' : 'mdi-window-close'"
                        ></v-icon>Zavarovanje odpovedi
                      </li>
                    </ul>
                  </v-card-text>
                </v-card>
              </v-flex>
            </v-layout>
          </v-expansion-panel-content>
        </v-expansion-panel>
      </v-layout>

    </v-flex>

    <!-- SHOWED ONLY ON WIDER SCREENS -->

    <v-flex class="offerDisplay2">
      <v-layout>
        <v-flex
          xs6
          class="offerDisplay212"
        >
          <v-flex xs12>
            <v-card>
              <v-card-title>
                <div class="text-xs-center">
                  <div class="title">BUDGET</div>
                  <div>{{offer.vehicle.deposit.amount}}€</div>
                  <div>{{offer.vehicle.deposit.amount/150}}€/dan</div>
                </div>
              </v-card-title>
              <v-card-text class="OfferListObject">
                <ul class="OfferList">
                  <li>
                    <v-icon
                      height="5"
                      v-text="neomejenaKilometrina ? 'mdi-check-outline' : 'mdi-window-close'"
                    ></v-icon>Neomejena kilometrina
                  </li>
                  <li>
                    <v-icon
                      height="5"
                      v-text="PolniKasko ? 'mdi-check-outline' : 'mdi-window-close'"
                    ></v-icon>Polno kasko zavarovanje
                  </li>
                  <li>
                    <v-icon
                      height="5"
                      v-text="StealCoverage ? 'mdi-check-outline' : 'mdi-window-close'"
                    ></v-icon>Zaščita pred krajo
                  </li>
                  <li>
                    <v-icon
                      height="5"
                      v-text="SuperExvessRefund ? 'mdi-check-outline' : 'mdi-window-close'"
                    ></v-icon>Super Excess Refund
                  </li>
                  <li>
                    <v-icon
                      height="5"
                      v-text="CancelEsuranse ? 'mdi-check-outline' : 'mdi-window-close'"
                    ></v-icon>Zavarovanje odpovedi
                  </li>
                </ul>
              </v-card-text>
            </v-card>
          </v-flex>
          <v-flex xs12>
            <v-layout>
              <v-flex justify-center>
                <v-btn
                  class="ChoosingCarBtn"
                  color="#e0714c"
                >
                  <span>IZBERITE AVTOMOBIL</span>
                </v-btn>
              </v-flex>
            </v-layout>
          </v-flex>
        </v-flex>

        <v-flex
          xs6
          class="offerDisplay212 OfferListObject__Border"
        >
          <v-card>
            <v-card-title>
              <div class="text-xs-center">
                <div class="title">RELAX</div>
                <div>{{offer.vehicle.deposit.amount}}€</div>
                <div>{{offer.vehicle.deposit.amount/150}}€/dan</div>
              </div>
            </v-card-title>
            <v-card-text class="OfferListObject">
              <ul class="OfferList">
                <li>
                  <v-icon
                    height="5"
                    v-text="neomejenaKilometrina ? 'mdi-check-outline' : 'mdi-window-close'"
                  ></v-icon>Neomejena kilometrina
                </li>
                <li>
                  <v-icon
                    height="5"
                    v-text="PolniKasko ? 'mdi-check-outline' : 'mdi-window-close'"
                  ></v-icon>Polno kasko zavarovanje
                </li>
                <li>
                  <v-icon
                    height="5"
                    v-text="StealCoverage ? 'mdi-check-outline' : 'mdi-window-close'"
                  ></v-icon>Zaščita pred krajo
                </li>
                <li>
                  <v-icon
                    height="5"
                    v-text="SuperExvessRefund ? 'mdi-check-outline' : 'mdi-window-close'"
                  ></v-icon>Super Excess Refund
                </li>
                <li>
                  <v-icon
                    height="5"
                    v-text="CancelEsuranse ? 'mdi-check-outline' : 'mdi-window-close'"
                  ></v-icon>Zavarovanje odpovedi
                </li>
              </ul>
            </v-card-text>
          </v-card>
          <v-layout>
            <v-flex justify-center>
              <v-btn
                class="ChoosingCarBtn"
                color="#e0714c"
                outline
              >
                <span>IZBERITE AVTOMOBIL</span>
              </v-btn>
            </v-flex>
          </v-layout>
        </v-flex>
      </v-layout>
    </v-flex>
  </v-layout>
</template>

<script>
export default {
  props: ['offer'],
  data () {
    return {
      // important informations about specific car
      neomejenaKilometrina: true,
      PolniKasko: true,
      StealCoverage: true,
      SuperExvessRefund: false,
      CancelEsuranse: false,
      dialog: false
    }
  }
}
</script>

<style lang="scss" scoped>
@mixin BiggerThan($breakpoint) {
  @if $breakpoint == md {
    @media only screen and (min-width: 960px) {
      @content;
    }
  }
}
@mixin SmallerThan($breakpoint) {
  @if $breakpoint == md {
    @media only screen and (max-width: 960px) {
      @content;
    }
  }
}

.v-expansion-panel {
  // max-width: 250px;
  -webkit-border-radius: 4px;
  -moz-border-radius: 4px;
  border-radius: 4px;
}

.expansionHeader {
  color: white;
  padding: -10px;
  margin: -8px;
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

// show buttons on smaller screens and hide them
// on bigger screens

.OfferButtons {
  @include BiggerThan(md) {
    display: none;
  }
}
.offerDisplay2 {
  width: 50%;
  height: 100%;
  @include SmallerThan(md) {
    display: none;
  }
}

.offerDisplay1 {
  width: 50%;
  @include SmallerThan(md) {
    width: 100%;
  }
}
.offerDisplay21 {
  width: 100px;
}
.OfferList {
  padding: 0px;
  margin: 1px;
  white-space: normal;
}
.OfferListObject {
  min-width: 180px;
  padding: 4px;
  margin: 0px;
  &__Border {
    border: 1px solid #a9be48;
    box-shadow: 0 0 4px 0 #a9be48;
  }
}

.CardInfoLink {
  color: #33a8d5;
  a {
    text-decoration: underline;
    cursor: pointer;
  }
}
.ValueOnIcons {
  color: gray;
  padding: 0px;
  margin: 0px;
}

// design selected car
.ChoosingCarBtn {
  width: 70%;
  height: 50px;
  span {
    white-space: normal;
  }
}
</style>
