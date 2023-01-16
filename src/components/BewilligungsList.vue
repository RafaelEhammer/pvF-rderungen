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
</template>
<script>
import { defineComponent, ref } from 'vue'

export default defineComponent({
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
  setup(props) {
    const editing = ref(false);
    const maxFoerdersumme = ref(10000000);

    function editCell(index) {
      editing.value = true;
    }
    function saveCell(index) {
      editing.value = false;
    }
    function cancelEdit() {
      editing.value = false;
    }

    return {
      antraege: props.antraege,
      changeBewilligung: props.changeBewilligung,
      maxFoerdersumme,
      editing,
      editCell,
      saveCell,
      cancelEdit
    }
  }
});
</script>

<style scoped>
/* Global Styles */
body {
  background-color: #f2e6ff;
}

/* Header Styles */
h1 {
  text-align: center;
  color: #383636;
  margin-top: 50px;
  margin-bottom: 30px;
}

/* Description Styles */
div {
  text-align: center;
  font-size: 1.2em;
  margin: 0 auto;
  width: 80%;
  color: #383636;
  padding-bottom: 30px;
}

/* Table Styles */
table {
  border-collapse: collapse;
  margin-left: auto;
  margin-right: auto;
  font-size: 0.9em;
  font-family: sans-serif;
  width: 100%;
  box-shadow: 0 0 20px rgba(153, 89, 182, 0.1);
}

th {
  text-align: center;
  background-color: #d6baf5;
  color: #383636;
  padding: 10px;
}

td {
  text-align: center;
  padding: 10px;
}

/* Form Styles */
input[type='text'],
input[type='number'] {
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  box-sizing: border-box;
  border: 2px solid #ccc;
  border-radius: 4px;
  background-color: #f8f8f8;
  font-size: 0.9em;
}

input[type='checkbox'] {
  margin-top: 20px;
}

input[type='text']:focus,
input[type='number']:focus {
  border: 2px solid #9b59b6;
}

button {
  width: 100%;
  background-color: #9b59b6;
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.9em;
}

button:hover {
  background-color: #8e44ad;
}

.editing-controls {
  text-align: center;
  margin-top: 20px;
}
</style>
