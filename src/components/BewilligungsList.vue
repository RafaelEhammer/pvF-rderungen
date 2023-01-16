<template>
  <div>
    <h1>PV - Fördererungen</h1>
    EAG-Investitionszuschuss Photovoltaik und Stromspeicher im Jahr 2023<br />
    Mit dem Erneuerbaren-Ausbau-Gesetz (EAG) wurden die rechtlichen
    Rahmenbedingungen für den Netzanschluss von erneuerbaren Energieanlagen
    vereinfacht. Dies umfasst auch finanzielleErleichterungen in Form eines
    pauschalierten Netzzutrittsentgelts. Mit einem der EAG-Investitionszuschüsse
    werden die Neuerrichtung und Erweiterung von Photovoltaikanlagen und die
    damit verbundene Neuerrichtung von Stromspeichern gefördert. Für die
    Erweiterung einer Photovoltaikanlage ist keine Mindestgröße vorgesehen.
    <hr />
    <h1>Bisherige Ansuchen (Max. Fördersumme {{ maxFoerdersumme }}€)</h1>
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>PLZ</th>
          <th>Zählpunkt</th>
          <th>KW-Peak</th>
          <th>bewilligt</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(ansuche, index) in antraege" :key="index">
          <td>{{ ansuche.name }}</td>
          <td>{{ ansuche.plz }}</td>
          <td @click="editCell(index)">
            <span v-if="!editing" v-text="ansuche.zaehlpunkt"></span>
            <input
              v-else
              v-model="ansuche.zaehlpunkt"
              @blur="saveCell(index)"
            />
          </td>
          <td @click="editCell(index)">
            <span v-if="!editing" v-text="ansuche.kwPeak"></span>
            <input v-else v-model="ansuche.kwPeak" @blur="saveCell(index)" />
          </td>
          <td>
            <input
              type="checkbox"
              @change="changeBewilligung(index)"
              :checked="ansuche.bewilligt"
            />
          </td>
        </tr>
      </tbody>
    </table>
    <div v-if="editing">
      <button @click="saveCell(index)">Save</button>
      <button @click="cancelEdit">Cancel</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    antraege: {
      type: Array,
      required: true,
    },
    changeBewilligung: {
      type: Function,
      required: true,
    },
  },
  data() {
    return {
      editing: false,
      maxFoerdersumme: 10000000,
    };
  },
  methods: {
    editCell(index) {
      this.editing = true;
    },
    saveCell(index) {
      this.editing = false;
      // Save the updated data here (e.g. by calling an API or updating a local data store)
    },
    cancelEdit() {
      this.editing = false;
      // Revert the changes here (e.g. by restoring the previous value from a local data store)
    },
  },
};
</script>

<style scoped>
h1 {
  text-align: center;
}
table {
  border-collapse: collapse;
  margin-left: auto;
  margin-right: auto;
  font-size: 0.9em;
  font-family: sans-serif;
  width: 100%;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.15);
}
thead tr {
  background-color: #009879;
  color: #ffffff;
  text-align: left;
}
th tr {
  padding: 12px 15px;
  width: 25%;
  text-align: center;
}
tbody tr {
  border-bottom: 1px solid #dddddd;
  color: #181818;
  background-color: blanchedalmond;
}
tbody tr:nth-of-type(even) {
  background-color: #f3f3f3;
}
tbody tr.active-row {
  font-weight: bold;
  color: #009879;
}
</style>
