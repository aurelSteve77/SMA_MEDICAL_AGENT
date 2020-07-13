<template>
  <div>
    <v-tabs v-model="tab" grow background-color="transparent" color="basil">
      <v-tab>
        Simulation
      </v-tab>

      <v-tab>
        Rapports
      </v-tab>
    </v-tabs>

    <v-tabs-items v-model="tab">
      <v-tab-item>
        <v-container>
          <v-row>
            <v-col cols="8">
              <v-row>
                <v-col cols="6">
                  <v-card>
                    <v-card-title class="text-center justify-center py-6">
                      <h5 class=" basil--text">
                        Patients en attente
                      </h5>
                    </v-card-title>
                    <v-card-text>
                      <v-simple-table height="150px">
                        <template v-slot:default>
                          <thead>
                            <tr>
                              <th class="text-left">Numéro</th>
                              <th class="text-left">Patient</th>
                              <th class="text-left"> Symptômes </th>
                            </tr>
                          </thead>
                          <tbody>
                            <tr>
                              <td>08</td>
                              <td> Boris </td>
                              <td> Aucun </td>
                            </tr>
                          </tbody>
                        </template>
                      </v-simple-table>
                    </v-card-text>
                  </v-card>
                </v-col>

                <v-col cols="6">
                  <v-card>
                    <v-card-title class="text-center justify-center py-6">
                      <h5 class=" basil--text">
                        Opérations caissières
                      </h5>
                    </v-card-title>
                    <v-card-text>
                      <v-simple-table height="150px">
                        <template v-slot:default>
                          <thead>
                            <tr>
                              <th class="text-left">Numéro</th>
                              <th class="text-left">Patient</th>
                              <th class="text-left"> Etat </th>
                            </tr>
                          </thead>
                          <tbody>
                            <tr>
                              <td>07</td>
                              <td>Steve</td>
                              <td> En cours </td>
                            </tr>
                          </tbody>
                        </template>
                      </v-simple-table>
                    </v-card-text>
                  </v-card>
                </v-col>
              </v-row>

              <v-row>
                <v-col cols="6">
                  <v-card>
                    <v-card-title class="text-center justify-center py-6">
                      <h5 class=" basil--text">
                        Consultations en cours
                      </h5>
                    </v-card-title>
                    <v-card-text>
                      <v-simple-table height="150px">
                        <template v-slot:default>
                          <thead>
                            <tr>
                              <th class="text-left">Numéro Medecin</th>
                              <th class="text-left">Numéro Patients</th>
                              <th class="text-left">Diagnostic</th>
                            </tr>
                          </thead>
                          <tbody>
                            <tr>
                              <td>01</td>
                              <td>11</td>
                              <td>Paludisme</td>
                            </tr>
                          </tbody>
                        </template>
                      </v-simple-table>
                    </v-card-text>
                  </v-card>
                </v-col>

                <v-col cols="6">
                  <v-card>
                    <v-card-title class="text-center justify-center py-6">
                      <h5 class=" basil--text">
                        Achats de medicaments en cours
                      </h5>
                    </v-card-title>
                    <v-card-text>
                      <v-simple-table height="150px">
                        <template v-slot:default>
                          <thead>
                            <tr>
                              <th class="text-left">N Patients</th>
                              <th class="text-left">Medicament</th>
                              <th class="text-left">Prix</th>
                            </tr>
                          </thead>
                          <tbody>
                            <tr>
                              <td>22</td>
                              <td>Paracétamol</td>
                              <td>500</td>
                            </tr>
                          </tbody>
                        </template>
                      </v-simple-table>
                    </v-card-text>
                  </v-card>
                </v-col>
              </v-row>
            </v-col>

            <v-col cols="4">
              <v-card height="530px">
                <v-card-title class="text-center justify-center py-6">
                  <h5 class=" basil--text">
                    Paramètres de la simulation
                  </h5>
                </v-card-title>
                <v-card-text>
                  <v-text-field
                    label="Nombre de Médécins"
                    filled
                  ></v-text-field>

                  <v-text-field
                    label="Nombre de Sécrétaires"
                    filled
                  ></v-text-field>

                  <v-text-field
                    label="Nombre d'infirmières"
                    filled
                  ></v-text-field>
                  <v-slider
                    max="3"
                    label="Arrivée clients"
                    step="1"
                    ticks="always"
                  ></v-slider>
                </v-card-text>
                <v-card-actions>
                  <v-btn color="basil" text>Modifier</v-btn>
                  <v-btn text color="teal lighten-1">Par défaut</v-btn>
                </v-card-actions>
              </v-card>
            </v-col>
          </v-row>

          <v-fab-transition>
              <v-btn
                v-show="!hidden"
                color="pink"
                dark
                absolute
                bottom
                right
                fab
              >
                <v-icon>mdi-run</v-icon>
              </v-btn>
            </v-fab-transition>
        </v-container>
      </v-tab-item>

      <v-tab-item>
        Tonton mon ami
      </v-tab-item>
    </v-tabs-items>
    
  </div>
</template>

<script>
const jssim = require("js-simulator");

// const simulation_constant = {
//   medicaments: [
//     {
//       name: "Bimalaril",
//       prixU: 2500,
//     },
//     {
//       name: "Chloroquine",
//       prixU: 1750,
//     },
//     {
//       name: "Paracétamol",
//       prixU: 500,
//     },
//   ],

//   symptomes: [
//     {
//       name: "Fièvre",
//     },
//     {
//       name: "Toux",
//     },
//     {
//       name: "Maux de tête",
//     },
//     {
//       name: "Manque d'appetit ",
//     },
//     {
//       name: "Selles liquides",
//     },
//     {
//       name: "anxiété",
//     },
//   ],

//   maladies: [
//     {
//       name: "Paludisme",
//       medicaments: [
//         {
//           name: "Bimalaril",
//         },
//       ],
//       must_cure: false,
//       symptomes: [
//         {
//           name: "Fièvre",
//         },
//         {
//           name: "Maux de tête",
//         },
//       ],
//     },

//     {
//       name: "Corona",
//       medicaments: [
//         {
//           name: "Chloroquine",
//         },
//       ],
//       must_cure: true,
//       symptomes: [
//         {
//           name: "Fièvre",
//         },
//         {
//           name: "Toux",
//         },
//       ],
//     },

//     {
//       name: "Diahrée",
//       medicaments: [
//         {
//           name: "Paracétamol",
//         },
//       ],
//       must_cure: false,
//       symptomes: [
//         {
//           name: "Selles liquides",
//         },
//       ],
//     },
//   ],
// };

export default {
  data: () => ({
    tab: null,

    sim_params: {
      num_medecins: 2,
      num_secreataires: 2,
      num_infirms: 2,
      num_pharmacies: 1,
      consultation_duration: 2,
      apparition_patient_duration: 2,
    },

    live_params: {
      client_number: 0,
      current_number: 0,
      consultation_list: [],
      facture_list: [],
      medic_payment_list: [],
    },
  }),

  methods: {
    runSimulation() {
      var scheduler = new jssim.Scheduler();
      var rank = 1;
      var evt = new jssim.SimEvent(rank);
      evt.id = 20;
      evt.update = function(deltaTime) {
        console.log(
          "event [" +
            this.id +
            "] with rank" +
            this.rank +
            " is fired at time " +
            this.time
        );
        console.log(deltaTime);
      };
      var time_to_fire = 10; // fire this event at time = 10
      scheduler.schedule(evt, time_to_fire);

      while (scheduler.hasEvents()) {
        scheduler.update();
      }
    },
  },
};
</script>

<style>
/* Helper classes */
.basil {
  background-color: #fffbe6 !important;
}
.basil--text {
  color: #356859 !important;
}
</style>
