<template>
  <div>
    <v-tabs v-model="tab" grow background-color="transparent" color="basil">
      <v-tab>
        Simulation
      </v-tab>

      <v-tab>
        Rapports
      </v-tab>

      <v-tab>
        Paramètres
      </v-tab>
    </v-tabs>

    <v-tabs-items v-model="tab">
      <v-tab-item>
        <v-container fluid>
          <v-row>
            <v-col cols="12">
              <v-row>
                <v-col cols="4">
                  <v-card>
                    <v-card-title class="text-center justify-center py-6">
                      <h5 class=" basil--text">
                        Patients en attente ({{ patient_waiting.length }})
                      </h5>
                    </v-card-title>
                    <v-card-text>
                      <v-simple-table height="175px">
                        <template v-slot:default>
                          <thead>
                            <tr>
                              <th class="text-left">Numéro</th>
                              <th class="text-left">Nom</th>
                              <th class="text-left">Symptômes</th>
                            </tr>
                          </thead>
                          <tbody>
                            <tr
                              v-for="patient in patient_waiting"
                              :key="patient.name"
                            >
                              <td>{{ patient.order_number }}</td>
                              <td>{{ patient.nom }}</td>
                              <td>{{ patient.symptomes }}</td>
                            </tr>
                          </tbody>
                        </template>
                      </v-simple-table>
                    </v-card-text>
                  </v-card>
                </v-col>

                <v-col cols="4">
                  <v-card>
                    <v-card-title class="text-center justify-center py-6">
                      <h5 class=" basil--text">
                        Caisses
                      </h5>
                    </v-card-title>
                    <v-card-text>
                      <v-simple-table height="175px">
                        <template v-slot:default>
                          <thead>
                            <tr>
                              <th class="text-left">N caissière</th>
                              <th class="text-left">N Patient</th>
                              <th class="text-left">Action</th>
                              <th class="text-left">Etat</th>
                            </tr>
                          </thead>
                          <tbody>
                            <tr
                              v-for="patient in patient_paying_fact"
                              :key="patient.patient.nom"
                            >
                              <td>{{ patient.caissiere.id }}</td>
                              <td>{{ patient.patient.nom }}</td>
                              <td>{{ patient.operation }}</td>
                              <td>{{ patient.etat }}</td>
                            </tr>
                          </tbody>
                        </template>
                      </v-simple-table>
                    </v-card-text>
                  </v-card>
                </v-col>

                <v-col cols="4">
                  <v-card>
                    <v-card-title class="text-center justify-center py-6">
                      <h5 class=" basil--text">
                        Consultations
                      </h5>
                    </v-card-title>
                    <v-card-text>
                      <v-simple-table height="175px">
                        <template v-slot:default>
                          <thead>
                            <tr>
                              <th class="text-left">N Medecin</th>
                              <th class="text-left">Patient</th>
                              <th class="text-left">Symptomes</th>
                              <th class="text-left">Examens</th>
                            </tr>
                          </thead>
                          <tbody>
                            <tr
                              v-for="item in patient_consulting"
                              :key="item.patient.nom"
                            >
                              <td>{{ item.medecin.id }}</td>
                              <td>{{ item.patient.nom }}</td>
                              <td>{{ item.patient.symptomes }}</td>
                              <td>{{ item.examen }}</td>
                            </tr>
                          </tbody>
                        </template>
                      </v-simple-table>
                    </v-card-text>
                  </v-card>
                </v-col>
              </v-row>

              <v-row>
                <v-col cols="4">
                  <v-card>
                    <v-card-title class="text-center justify-center py-6">
                      <h5 class=" basil--text">
                        Laboratoires
                      </h5>
                    </v-card-title>
                    <v-card-text>
                      <v-simple-table height="175px">
                        <template v-slot:default>
                          <thead>
                            <tr>
                              <th class="text-left">N Laborantin</th>
                              <th class="text-left">Patient</th>
                              <th class="text-left">Examen</th>
                              <th class="text-left">Verdict</th>
                            </tr>
                          </thead>
                          <tbody>
                            <tr v-for="item in patient_examining" :key="item.patient.nom">
                              <td>{{item.laborantin.id}}</td>
                              <td>{{item.patient.nom}}</td>
                              <td>{{item.examen}}</td>
                              <td>{{item.maladie}}</td>
                            </tr>
                          </tbody>
                        </template>
                      </v-simple-table>
                    </v-card-text>
                  </v-card>
                </v-col>

                <v-col cols="4">
                  <v-card>
                    <v-card-title class="text-center justify-center py-6">
                      <h5 class=" basil--text">
                        Pharmacies
                      </h5>
                    </v-card-title>
                    <v-card-text>
                      <v-simple-table height="175px">
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

                <v-col cols="4">
                  <v-card>
                    <v-card-title class="text-center justify-center py-6">
                      <h5 class=" basil--text">
                        Notifications
                      </h5>
                    </v-card-title>
                    <v-card-text>
                      <v-simple-table height="175px" dark>
                        <template v-slot:default>
                          <thead>
                            <tr>
                              <th class="text-left">Numéro</th>
                              <th class="text-left">Message</th>
                            </tr>
                          </thead>
                          <tbody>
                            <tr
                              v-for="notif in notifications_messages"
                              :key="notif.id"
                            >
                              <td>{{ notif.id }}</td>
                              <td>{{ notif.message }}</td>
                            </tr>
                          </tbody>
                        </template>
                      </v-simple-table>
                    </v-card-text>
                  </v-card>
                </v-col>
              </v-row>
            </v-col>
          </v-row>

          <v-fab-transition>
            <v-btn
              v-show="!hidden"
              color="pink"
              dark
              absolute
              top
              right
              fab
              v-on:click="runSimulation"
            >
              <v-icon>mdi-run</v-icon>
            </v-btn>
          </v-fab-transition>
        </v-container>
      </v-tab-item>

      <v-tab-item>
        Tonton mon ami
      </v-tab-item>

      <v-tab-item>
        <v-container>
          <v-col cols="4">
            <v-card height="530px">
              <v-card-title class="text-center justify-center py-6">
                <h5 class=" basil--text">
                  Paramètres de la simulation
                </h5>
              </v-card-title>
              <v-card-text>
                <v-text-field label="Nombre de Médécins" filled></v-text-field>

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
        </v-container>
      </v-tab-item>
    </v-tabs-items>
  </div>
</template>

<script>
/* eslint-disable no-unused-vars */
const jssim = require("js-simulator");
const randomNameGenerator = require("random-name");
const UNIT_TIME = 60;

//base de connaissances
const symptomes = [
  "fievre",
  "toux seche",
  "fatigue",
  "maux de tete",
  "douleur musculaire",
  "affaiblissement",
  "vomissements",
  "diarrhé",
  "toux",
  "douleur abdominale",
  "ballonement",
  "perte d'appetit",
];

const examen = [
  "test du paludisme",
  "test du covid-19",
  "test de la thyphoide",
];
const maladie = ["paludisme", "covid-19", "thyphoide"];
const corona = ["fievre", "toux seche", "fatigue"];
const paludisme = [
  "fievre",
  "maux de tete",
  "douleur musculaire",
  "affaiblissement",
  "vomissements",
  "diarrhé",
  "toux",
];
const thyphoide = [
  "fievre",
  "fatigue",
  "maux de tete",
  "douleur musculaire",
  "vomissements",
  "diarrhé",
  "douleur abdominale",
  "ballonement",
];

function getRandomInt(max) {
  return Math.floor(Math.random() * Math.floor(max));
}

//var nb=  getRandomInt(symptomes.length+1);

var symptome_patient = function(symptomes, nb) {
  var result = [];
  for (var i = 0; i < nb; i++) {
    result.push(symptomes[Math.floor(Math.random() * symptomes.length)]);
  }
  return result;
};

function exam_list(symptome_) {
  var todo_exams = [];
  var len = symptome_.length;

  if (len == 0) {
    return todo_exams;
  } else {
    var corona_match = 0;
    var paludisme_match = 0;
    var thyphoide_match = 0;
    for (var i = 0; i < len; i++) {
      //on vérifie si le symptome est dans les symptomes de corona
      var j = 0;
      while (corona[j] !== symptome_[i] && j <= corona.length) {
        j++;
      }
      if (j <= corona.length) {
        corona_match++;
      }
      //on vérifie si le symptome est dans les symptomes du palu
      j = 0;
      while (paludisme[j] !== symptome_[i] && j <= paludisme.length) {
        j++;
      }
      if (j <= paludisme.length) {
        paludisme_match++;
      }
      //on vérifie si le symptome est dans les symptomes de la thyphoide
      j = 0;
      while (thyphoide[j] !== symptome_[i] && j <= thyphoide.length) {
        j++;
      }
      if (j <= thyphoide.length) {
        thyphoide_match++;
      }
    }

    var max = Math.max(corona_match, paludisme_match, thyphoide_match);

    if (corona_match == max) {
      todo_exams.push("corona");
    }
    if (paludisme_match == max) {
      todo_exams.push("paludisme");
    }
    if (thyphoide_match == max) {
      todo_exams.push("thyphoide");
    }

    return todo_exams;
  }
}

function maladie_() {
  var i = exam_list(symptome_patient).length;
  if (i == 0) {
    return "pas de maladie";
  }
  if (i == 1) {
    return exam_list(symptome_patient)[0];
  }
  if (i > 1) {
    return exam_list(symptome_patient)[getRandomInt(i)];
  }
}

function move_free(item, liste, free) {
  if (free) {
    liste.libres.push(item);
    let index = liste.occupes.indexOf(item);
    if (index > -1) {
      liste.occupes.splice(index, 1);
    }
  } else {
    liste.occupes.push(item);
    let index = liste.libres.indexOf(item);
    if (index > -1) {
      liste.libres.splice(index, 1);
    }
  }
}

const MESSAGE_TYPE = {
  MEDECIN: {
    SEND_PATIENT: "SEND_PATIENT",
  },
  CASSIERE: {
    GO_MEDECIN: "GO_MEDECIN",
    CAME_PAY: "CAME_PAY",
  },
  PATIENT: {
    PAY_CONSULT: "PAY_CONSULT",
    CONSULT_ME: "CONSULT_ME",
  },
  LABORATIN: {
    EXAM_AVAILABLE: "EXAM_AVAILABLE"
  }
};

//fonctions utiles
function createNotification(message, table) {
  table.unshift({ id: table.length, message: message });
}

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

    patient_waiting: [],
    patient_paying_fact: [],
    patient_consulting: [],
    patient_examining: [],

    medecins: {
      libres: [],
      occupes: [],
    },

    caissieres: {
      libres: [],
      occupes: [],
    },

    laboratoires: {
      libres: [],
      occupes: [],
    },

    pharmacies: {
      libres: [],
      occupes: [],
    },

    notifications_messages: [],

    live_params: {
      client_number: 0,
      current_number: 0,
      consultation_list: [],
      facture_list: [],
      medic_payment_list: [],
    },
  }),

  methods: {
    generateNamed() {
      console.log(randomNameGenerator.first());
    },

    runSimulation() {
      //definition des variables
      var patient_waiting = this.patient_waiting;
      var patient_paying_fact = this.patient_paying_fact;
      var patient_consulting = this.patient_consulting;
      var patient_examining = this.patient_examining;

      var notifications_list = this.notifications_messages;
      var medecins_list = this.medecins;
      var caissieres_list = this.caissieres;
      var laboratoires_list = this.laboratoires;
      var pharmacie_list = this.pharmacies;
      var max_number = 0;

      //ordonnanceur
      var scheduler = new jssim.Scheduler();
      scheduler.reset();

      /*  ------------AGENTS-------------  */

      //agent patient
      var PatientAgent = function(name, symptomes) {
        jssim.SimEvent.call(this, 1);
        this.symptomes = symptomes;
        this.nom = name;
        this.order_number = -1;
      };
      PatientAgent.prototype = Object.create(jssim.SimEvent.prototype);
      PatientAgent.prototype.update = function(deltaTime) {
        //check de message
        let inbox_messages = this.readInBox();
        for (let i = 0; i < inbox_messages.length; i++) {
          this.message_incourse = false;
          let msg = inbox_messages[i];
          let sender_id = msg.sender;
          let msg_type = msg.type;
          let notif_message = "";
          switch (msg_type) {
            case MESSAGE_TYPE.CASSIERE.CAME_PAY:
              this.order_number = msg.content;
              this.sendMsg(sender_id, {
                type: MESSAGE_TYPE.PATIENT.PAY_CONSULT,
                content: this.nom,
              });
              break;
            case MESSAGE_TYPE.MEDECIN.SEND_PATIENT:
              this.sendMsg(msg.med_id, {
                type: MESSAGE_TYPE.PATIENT.CONSULT_ME,
                content: msg.content,
                symptomes: this.symptomes,
              });
              break;
            case MESSAGE_TYPE.LABORATIN.EXAM_AVAILABLE:
              console.log('Je souffre de', msg.content.maladie);
              break;
          }
        }
      };

      //agent caissière
      var CaissiereAgent = function(id) {
        jssim.SimEvent.call(this);
        this.libre = true;
        this.id = id;
        this.current_service = null;
        this.medecin_waiting = {
          in_course: false,
          msg_content: null,
          med_id: null,
        };
      };
      CaissiereAgent.prototype = Object.create(jssim.SimEvent.prototype);
      CaissiereAgent.prototype.update = function(deltaTime) {
        if (this.libre) {
          //appeler un patient pour lui donner un numéro
          //TODO MOVE PATIENT TO CAISSE
          if (patient_waiting.length != 0) {
            let pat = patient_waiting.shift();
            let patient_id = pat.guid();
            this.current_service = {
              patient: pat,
              caissiere: this,
              operation: "Payer Consultation",
              etat: "en cours",
            };
            patient_paying_fact.unshift(this.current_service);
            this.sendMsg(patient_id, {
              type: MESSAGE_TYPE.CASSIERE.CAME_PAY,
              content: max_number,
            });
            max_number += 1;
            this.libre = false;
            move_free(this, caissieres_list, this.libre);
          }
        }

        let inbox_messages = this.readInBox();
        for (let i = 0; i < inbox_messages.length; i++) {
          let msg = inbox_messages[i];
          let sender_id = msg.sender;
          let recipient_id = msg.recipient;
          let msg_type = msg.type;
          switch (msg_type) {
            case MESSAGE_TYPE.PATIENT.PAY_CONSULT:
              //TODO SAVE TO CONSULTATION PAY LIST
              //TODO show notification
              this.current_service.etat = "Finish";
              this.libre = true;
              move_free(this, caissieres_list, this.libre);
              break;
            case MESSAGE_TYPE.MEDECIN.SEND_PATIENT:
              if (
                patient_paying_fact.length != 0 &&
                patient_paying_fact[patient_paying_fact.length - 1].etat ==
                  "Finish"
              ) {
                console.log("Que oohh j'ai trouvé un gar a send");

                let patient = patient_paying_fact.shift();
                let patient_consult_item = {
                  patient: patient.patient,
                  medecin: msg.content,
                  examen: "EN COURS",
                };
                patient_consulting.unshift(patient_consult_item);
                this.sendMsg(patient.patient.guid(), {
                  type: MESSAGE_TYPE.MEDECIN.SEND_PATIENT,
                  content: patient_consult_item,
                  med_id: sender_id,
                });
                this.medecin_waiting = {
                  in_course: false,
                  msg_content: null,
                  med_id: null,
                };
              } else {
                this.medecin_waiting = {
                  in_course: true,
                  msg_content: msg.content,
                  med_id: sender_id,
                };
              }
              break;
          }
        }

        if (this.medecin_waiting.in_course) {
          if (
            patient_paying_fact.length != 0 &&
            patient_paying_fact[patient_paying_fact.length - 1].etat == "Finish"
          ) {
            let patient = patient_paying_fact.shift();
            let patient_consult_item = {
              patient: patient.patient,
              medecin: this.medecin_waiting.msg_content,
              examen: "EN COURS",
            };

            patient_consulting.unshift(patient_consult_item);
            this.sendMsg(patient.patient.guid(), {
              type: MESSAGE_TYPE.MEDECIN.SEND_PATIENT,
              content: patient_consult_item,
              med_id: this.medecin_waiting.med_id,
            });
            this.medecin_waiting = this.medecin_waiting = {
              in_course: false,
              msg_content: null,
              med_id: null,
            };
          }
        }
      };

      //apparitions des clients dans la clinique
      var patient_spawn_evt = new jssim.SimEvent(1);
      patient_spawn_evt.id = 1;
      patient_spawn_evt.update = function(deltaTime) {
        var name = randomNameGenerator.first();
        var patient = new PatientAgent(name, []);
        var start_time = 12;
        patient_waiting.push(patient);
        let notif_message = name + " est arrivé";
        createNotification(notif_message, notifications_list);
        scheduler.scheduleRepeatingAt(patient, scheduler.current_time, 60);
      };

      //agent medecin
      var MedecinAgent = function(id) {
        jssim.SimEvent.call(this);
        this.id = id;
        this.libre = true;
      };
      MedecinAgent.prototype = Object.create(jssim.SimEvent.prototype);
      MedecinAgent.prototype.update = function(deltaTime) {
        var inbox_messages = this.readInBox();
        for(var i = 0 ; i < inbox_messages.length; i++){
          let msg = inbox_messages[i];
          let msg_type = msg.type;
          let sender_id = msg.sender;

          switch(msg_type){
            case MESSAGE_TYPE.PATIENT.CONSULT_ME:
              var examen = exam_list(msg.symptomes);
              //TODO SAVE CONSULTATION
              msg.content.examen = examen;
              this.libre = true;
              break;
          }
          
        }

        if (this.libre) {
          let caissiere_id = caissiere1.guid();
          this.sendMsg(caissiere_id, {
            type: MESSAGE_TYPE.MEDECIN.SEND_PATIENT,
            content: this,
          });
          this.libre = false;
          move_free(this, medecins_list, this.libre);
        }
      };

      var LaboAgent = function(id) {
        jssim.SimEvent.call(this);
        this.id = id;
        this.libre = true;
        this.current_patient = null;
      };
      LaboAgent.prototype = Object.create(jssim.SimEvent.prototype);
      LaboAgent.prototype.update = function(deltaTime){
        if(this.libre){
          if(patient_consulting.length !=0 && 
          patient_consulting[patient_consulting.length-1].examen !="EN COURS"){
            var patient_exam_item = patient_consulting.shift();
            patient_exam_item.maladie = "En cours ...";
            patient_exam_item.laborantin = this;
            patient_examining.unshift(patient_exam_item);
            this.current_patient = patient_exam_item;
            this.libre = false;
          }
          else{
            this.current_patient.maladie = "PALU";
            this.sendMsg(this.current_patient.patient.guid(), {
              type: MESSAGE_TYPE.LABORATIN.EXAM_AVAILABLE,
              content: this.current_patient,
            })
            this.libre = true;
          }
        }
      }

      var caissiere1 = new CaissiereAgent(777);
      var caissiere2 = new CaissiereAgent(7777);
      var medecin1 = new MedecinAgent(33);
      var laborantin1 = new LaboAgent(27);

      this.medecins.libres.push(medecin1);
      this.caissieres.libres.push(caissiere1);
      this.caissieres.libres.push(caissiere2);
      

      scheduler.scheduleRepeatingAt(caissiere1, 0, 3 * UNIT_TIME);
      scheduler.scheduleRepeatingAt(caissiere2, 0, 3 * UNIT_TIME);
      scheduler.scheduleRepeatingAt(medecin1, 0, 3 * UNIT_TIME);
      scheduler.scheduleRepeatingAt(laborantin1, 0, 3 * UNIT_TIME);
      scheduler.scheduleRepeatingAt(patient_spawn_evt, 0, 7 * UNIT_TIME);

      setInterval(() => {
        scheduler.update();
      }, 1000);
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
