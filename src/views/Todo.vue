<template>
  <div class="home pa-12">
    <h1>To-Do page</h1>

    <v-btn
      class="white--text mt-4 ml-4"
      color="rgba(191, 78, 137)"
      v-if="!vidljiv"
      @click="vidljiv = !vidljiv"
    >
      + ADD
    </v-btn>
    <v-col :cols="5">
      <v-row class="w-50">
        <v-text-field
          v-if="vidljiv"
          v-model="inputZadatak"
          :rules="inputRules"
          label="New task"
          required
          @keyup.enter="dodajNoviZadatak"
          color="rgba(191, 78, 137)"
          class="ml-4 mb-2 mt-4"
        >
        </v-text-field>
        <v-btn
          small
          class="white--text ml-4 mt-7"
          color="rgba(191, 78, 137)"
          v-if="vidljiv"
          @click="dodajNoviZadatak()"
        >
          CONFIRM
        </v-btn>
      </v-row>
    </v-col>

    <v-list flat subheader>
      <div v-for="zadatak in zadatci" :key="zadatak.id">
        <v-list-item>
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox
                :input-value="zadatak.obavljeno"
                color="rgba(191, 78, 137)"
                @click="zadatak.obavljeno = !zadatak.obaveljeno"
              ></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title>{{ zadatak.naziv }}</v-list-item-title>
            </v-list-item-content>
            <v-icon color="rgba(191, 78, 137)" @click="izbrisi(zadatak.id)">
              mdi-trash-can
            </v-icon>
          </template>
        </v-list-item>
        <v-divider> </v-divider>
      </div>
    </v-list>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "Todo",
  data() {
    return {
      valid: false,
      inputZadatak: "",
      inputRules: [(v) => !!v || "Task is required"],
      vidljiv: false,
      zadatci: [
        /* {
          id: 1,
          naziv: "Cook ",
          obavljeno: false,
        },
        {
          id: 2,
          naziv: "Wake up ",
          obavljeno: false,
        },
        {
          id: 3,
          naziv: "Eat something ",
          obavljeno: false,
        },
        {
          id: 4,
          naziv: "Call brother ",
          obavljeno: false,
        },*/
      ],
    };
  },
  methods: {
    izbrisi(id_zadatka) {
      console.log("Brisanje zadatka");
      this.zadatci = this.zadatci.filter(
        (zadatak) => zadatak.id !== id_zadatka
      );
    },

    zadatakObavljen(id_zadatka) {
      console.log("Zadatak obavljen");
      this.zadatci = this.zadatci.filter(
        (zadatak) => zadatak.id === id_zadatka
      );
    },
    dodajNoviZadatak() {
      let noviZadatak = {
        id: Date.now(),
        naziv: this.inputZadatak,
        obavljeno: false,
      };
      this.zadatci.push(noviZadatak);
      console.log("Dodan zadatak");
      this.inputZadatak = "";
      this.vidljiv = !this.vidljiv;
    },
  },
};
</script>
<style scoped></style>
