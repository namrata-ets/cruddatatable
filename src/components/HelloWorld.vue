<!-- eslint-disable vue/valid-v-slot -->

<template>
  <v-container>
    <v-data-table
      :headers="headers"
      :items="passengers"
      sort-by="trips"
      class="elevation-1"
    >
      <template v-slot:top>
        <v-toolbar flat>
          <v-toolbar-title>Airline Reservation</v-toolbar-title>
          <v-divider class="mx-4" inset vertical></v-divider>
          <v-spacer></v-spacer>
          <v-dialog v-model="dialog" max-width="500px">
            <template v-slot:activator="{ on, attrs }">
              <v-btn color="primary" dark class="mb-2" v-bind="attrs" v-on="on">
                New Passenger
              </v-btn>
            </template>
            <v-card>
              <v-card-title>
                <span class="text-h5">{{ formTitle }}</span>
              </v-card-title>

              <v-card-text>
                <v-container>
                  <v-row>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field
                        v-model="editedItem.airline"
                        label="Airline name"
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field
                        v-model="editedItem.trips"
                        label="No Of Trips"
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field
                        v-model="editedItem.name"
                        label="Passenger Name"
                      ></v-text-field>
                    </v-col>
                  </v-row>
                </v-container>
              </v-card-text>

              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="blue darken-1" text @click="close">
                  Cancel
                </v-btn>
                <v-btn color="blue darken-1" text @click="save">
                  Save
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>
          <v-dialog v-model="dialogDelete" max-width="500px">
            <v-card>
              <v-card-title class="text-h5"
                >Are you sure you want to delete this item?</v-card-title
              >
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="blue darken-1" text @click="closeDelete"
                  >Cancel</v-btn
                >
                <v-btn color="blue darken-1" text @click="deleteItemConfirm"
                  >OK</v-btn
                >
                <v-spacer></v-spacer>
              </v-card-actions>
            </v-card>
          </v-dialog>
        </v-toolbar>
      </template>
      <template v-slot:item.actions="{ item }">
        <v-icon small class="mr-2" @click="editItem(item)">
          mdi-pencil
        </v-icon>
        <v-icon small @click="deleteItem(item)">
          mdi-delete
        </v-icon>
      </template>
      <template v-slot:no-data>
        <v-btn color="primary" @click="initialize">
          Reset
        </v-btn>
      </template>
    </v-data-table>
   
  </v-container>
</template>
<script>
export default {
  data: () => ({
    dialog: false,
    dialogDelete: false,
    headers: [
      {
        text: "Airline Name",
        align: "start",
        sortable: false,
        value: "airline",
      },
      { text: "Number of Trips", value: "trips" },
      { text: "Passenger Name", value: "name" },

      { text: "Actions", value: "actions", sortable: false },
    ],
    passengers: [],
    editedIndex: -1,
    editedItem: {
      name: "",
      trips: 0,
      airline: 0,
    },
    defaultItem: {
      name: "",
      trips: 0,
      airline: 0,
    },
  }),

  computed: {
    formTitle() {
      return this.editedIndex === -1 ? "New Passenger" : "Edit Passenger";
    },
  },

  watch: {
    dialog(val) {
      console.log(val);
      val || this.close();
    },
    dialogDelete(val) {
      val || this.closeDelete();
    },
  },

  created() {
    this.initialize();
  },

  methods: {
    initialize() {
      this.passengers = [
        {
          _id: "63e34c2d87ade9831e0cbd69",
          name: "Harish",
          trips: 230,
          airline: [
            {
              id: 4,
              name: "Emirates",
              country: "Dubai",
              logo:
                "https://upload.wikimedia.org/wikipedia/commons/thumb/d/d0/Emirates_logo.svg/150px-Emirates_logo.svg.png",
              slogan: "From Dubai to destinations around the world.",
              head_quaters: "Garhoud, Dubai, United Arab Emirates",
              website: "www.emirates.com/",
              established: "1985",
            },
          ],
          __v: 0,
        },
        {
          _id: "63e34c2e87ade91cd70cbd6d",
          name: "RAJESH",
          trips: 234,
          airline: [
            {
              id: 5,
              name: "Eva Air",
              country: "Taiwan",
              logo:
                "https://upload.wikimedia.org/wikipedia/en/thumb/e/ed/EVA_Air_logo.svg/250px-EVA_Air_logo.svg.png",
              slogan: "Sharing the World, Flying Together",
              head_quaters:
                "376, Hsin-Nan Rd., Sec. 1, Luzhu, Taoyuan City, Taiwan",
              website: "www.evaair.com",
              established: "1989",
            },
          ],
          __v: 0,
        },
        {
          _id: "63e34c2e87ade912620cbd6f",
          name: "AJITHA",
          trips: 345,
          airline: [
            {
              id: 9,
              name: "Japan Airlines",
              country: "Japan",
              logo:
                "https://upload.wikimedia.org/wikipedia/en/thumb/d/dd/Japan_Airlines_Logo_%282011%29.svg/300px-Japan_Airlines_Logo_%282011%29.svg.png",
              slogan: "Fly into tomorrow",
              head_quaters: "Shinagawa, Tokyo, Japan",
              website: "www.jal.com",
              established: "1951",
            },
          ],
          __v: 0,
        },
        {
          _id: "63e34c2e87ade9b1030cbd72",
          name: "Harish",
          trips: 230,
          airline: [
            {
              id: 4,
              name: "Emirates",
              country: "Dubai",
              logo:
                "https://upload.wikimedia.org/wikipedia/commons/thumb/d/d0/Emirates_logo.svg/150px-Emirates_logo.svg.png",
              slogan: "From Dubai to destinations around the world.",
              head_quaters: "Garhoud, Dubai, United Arab Emirates",
              website: "www.emirates.com/",
              established: "1985",
            },
          ],
          __v: 0,
        },
        {
          _id: "63e34c2e87ade911bd0cbd76",
          name: "AJIT",
          trips: 345,
          airline: [
            {
              id: 9,
              name: "Japan Airlines",
              country: "Japan",
              logo:
                "https://upload.wikimedia.org/wikipedia/en/thumb/d/dd/Japan_Airlines_Logo_%282011%29.svg/300px-Japan_Airlines_Logo_%282011%29.svg.png",
              slogan: "Fly into tomorrow",
              head_quaters: "Shinagawa, Tokyo, Japan",
              website: "www.jal.com",
              established: "1951",
            },
          ],
          __v: 0,
        },
        {
          _id: "63e34c2e87ade932fd0cbd78",
          name: "RAJESH",
          trips: 234,
          airline: [
            {
              id: 5,
              name: "Eva Air",
              country: "Taiwan",
              logo:
                "https://upload.wikimedia.org/wikipedia/en/thumb/e/ed/EVA_Air_logo.svg/250px-EVA_Air_logo.svg.png",
              slogan: "Sharing the World, Flying Together",
              head_quaters:
                "376, Hsin-Nan Rd., Sec. 1, Luzhu, Taoyuan City, Taiwan",
              website: "www.evaair.com",
              established: "1989",
            },
          ],
          __v: 0,
        },
        {
          _id: "63e34c2e87ade943f10cbd7b",
          name: "Harish",
          trips: 230,
          airline: [
            {
              id: 4,
              name: "Emirates",
              country: "Dubai",
              logo:
                "https://upload.wikimedia.org/wikipedia/commons/thumb/d/d0/Emirates_logo.svg/150px-Emirates_logo.svg.png",
              slogan: "From Dubai to destinations around the world.",
              head_quaters: "Garhoud, Dubai, United Arab Emirates",
              website: "www.emirates.com/",
              established: "1985",
            },
          ],
          __v: 0,
        },
        {
          _id: "63e34c2e87ade90baf0cbd7f",
          name: "RAJESH",
          trips: 234,
          airline: [
            {
              id: 5,
              name: "Eva Air",
              country: "Taiwan",
              logo:
                "https://upload.wikimedia.org/wikipedia/en/thumb/e/ed/EVA_Air_logo.svg/250px-EVA_Air_logo.svg.png",
              slogan: "Sharing the World, Flying Together",
              head_quaters:
                "376, Hsin-Nan Rd., Sec. 1, Luzhu, Taoyuan City, Taiwan",
              website: "www.evaair.com",
              established: "1989",
            },
          ],
          __v: 0,
        },
        {
          _id: "63e34c2e87ade969e30cbd81",
          name: "AJITHA",
          trips: 345,
          airline: [
            {
              id: 9,
              name: "Japan Airlines",
              country: "Japan",
              logo:
                "https://upload.wikimedia.org/wikipedia/en/thumb/d/dd/Japan_Airlines_Logo_%282011%29.svg/300px-Japan_Airlines_Logo_%282011%29.svg.png",
              slogan: "Fly into tomorrow",
              head_quaters: "Shinagawa, Tokyo, Japan",
              website: "www.jal.com",
              established: "1951",
            },
          ],
          __v: 0,
        },
        {
          _id: "63e34e0187ade954e10cbe18",
          name: "Prashant",
          trips: 25,
          airline: [
            {
              id: 5,
              name: "Eva Air",
              country: "Taiwan",
              logo:
                "https://upload.wikimedia.org/wikipedia/en/thumb/e/ed/EVA_Air_logo.svg/250px-EVA_Air_logo.svg.png",
              slogan: "Sharing the World, Flying Together",
              head_quaters:
                "376, Hsin-Nan Rd., Sec. 1, Luzhu, Taoyuan City, Taiwan",
              website: "www.evaair.com",
              established: "1989",
            },
          ],
          __v: 0,
        },
      ];
    },

    editItem(item) {
      this.editedIndex = this.passengers.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialog = true;
    },

    deleteItem(item) {
      this.editedIndex = this.passengers.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialogDelete = true;
    },

    deleteItemConfirm() {
      this.passengers.splice(this.editedIndex, 1);
      this.closeDelete();
    },

    close() {
      this.dialog = false;
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      });
    },

    closeDelete() {
      this.dialogDelete = false;
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      });
    },

    save() {
      if (this.editedIndex > -1) {
        Object.assign(this.passengers[this.editedIndex], this.editedItem);
      } else {
        this.passengers.push(this.editedItem);
      }
      this.close();
    },
  },
};
</script>
