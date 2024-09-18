<template>
  <div class="w-full h-screen">
    <div
      class="flex justify-center bg-white px-10 py-32 sm:p-32 text-slate-800 dark:bg-green-300 dark:text-slate-900 h-full">
      <Tabs>
        <Tab tab_title="First Tab">
          <div class="w-full h-full  p-2">
            <div class="w-full grid  grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4">
              <BasicInput :label="'label 1'" v-model="input1" error errorMessage="input Requerido" placeholder="e.g" />
              <BasicInput :label="'label 1'" error errorMessage="input Requerido" placeholder="e.g" />
              <!-- Note: password input falta la validación para emitir el evento de update:ModelValue  y obtener el valor por defecto. -->
              <PasswordInput label="Password" error errorMessage="input Requerido" placeholder="e.g" />
              <BasicInput :label="'label 1'" actionButtonSlot error errorMessage="input Requerido" placeholder="e.g">
                <template #InputButton>
                  <div class="flex w-full h-full bg-red-900">
                    <button class="w-full bg-gray-100 hover:bg-gray-200" @click="">
                      aa
                    </button>
                  </div>
                </template>
              </BasicInput>
              <Switch :label="'label 1'" text_On="SI" text_Off="No" v-model="switchToggle" />
              <BasicInput :label="'label 1'" />
              <BasicInput :label="'label 1'" />
              <BasicInput :label="'label 1'" />
              <BasicInput :label="'label 1'" />
              <BasicInput :label="'label 1'" />
              <BasicInput :label="'label 1'" />
              <BasicInput :label="'label 1'" />
              <BasicInput :label="'label 1'" />
              <BasicInput :label="'label 1'" />
              <BasicInput :label="'label 1'" />
              <BasicInput :label="'label 1'" />
              <BasicInput :label="'label 1'" />
              <BasicInput :label="'label 1'" />
            </div>
            <div class="w-full">
              <button class="p-2 bg-red-900 rounded-md text-white" @click="showData">Button</button>
            </div>
          </div>

        </Tab>
        <Tab active tab_title="Second Tab">
          <div class="w-full h-full p-2 ">
            <DataTable hover :items="items" :fields="fields" :numberItems="false" search />
          </div>
        </Tab>
        <Tab tab_title="Third Tab">
          Third Tab content
        </Tab>
        <Tab tab_title="Fourth Tab">
          Fourth Tab content
        </Tab>
        <Tab tab_title="Fifth Tab">
          Fifth Tab content
        </Tab>
      </Tabs>
    </div>
  </div>

</template>
<script setup>
import { ref } from 'vue'
// import Tabs from '@/components/UiComponents/TabsBCK/Tabs.vue';
// import Tab from '@/components/UiComponents/TabsBCK/Tab.vue'
import Tabs from '@/components/UiComponents/Tabs/Tabs.vue';
import Tab from '@/components/UiComponents/Tabs/Tab.vue';
import BasicInput from '@/components/UiComponents/InputsComponents/BasicInput.vue';
import PasswordInput from '@/components/UiComponents/InputsComponents/PasswordInput.vue';
import Switch from '@/components/UiComponents/Toggles/Switch.vue';
import DataTable from '@/components/UiComponents/Tables/DataTable.vue';
const input1 = ref('')
const switchToggle = ref(false)
const error = true
const showData = () => {
  console.log(switchToggle.value)
}

const items = ref([
  { "id": 1, "extension": 2951, "name": "Bartholomew Eggleson" },
  { "id": 2, "extension": 5718, "name": "Eldridge Aslen" },
  { "id": 3, "extension": 6505, "name": "Philippine Brayn" },
  { "id": 4, "extension": 4225, "name": "Ardine Warden" },
  { "id": 5, "extension": 1036, "name": "Nara Liverseege" },
  { "id": 6, "extension": 3597, "name": "Krystalle Vasyunichev" },
  { "id": 7, "extension": 1404, "name": "Anabal Bastistini" },
  { "id": 8, "extension": 4179, "name": "Edward Akam" },
  { "id": 9, "extension": 4417, "name": "Aguistin Gasker" },
  { "id": 10, "extension": 4666, "name": "Carleton Fink" },
  { "id": 11, "extension": 4941, "name": "Christin Ewbach" },
  { "id": 12, "extension": 3245, "name": "Adelaida Sumption" },
  { "id": 13, "extension": 4554, "name": "Lavinia Johns" },
  { "id": 14, "extension": 1222, "name": "Dani O'Hogertie" },
  { "id": 15, "extension": 2342, "name": "Karin Wiskar" },
  { "id": 16, "extension": 2121, "name": "Car Archley" },
  { "id": 17, "extension": 4680, "name": "Linn Pitrelli" },
  { "id": 18, "extension": 3806, "name": "Ronny Highton" },
  { "id": 19, "extension": 5489, "name": "Leodora Patullo" },
  { "id": 20, "extension": 6351, "name": "Corry Goly" },
  { "id": 21, "extension": 1730, "name": "Romain Ulyat" },
  { "id": 22, "extension": 2647, "name": "Clarey Forsyde" },
  { "id": 23, "extension": 6421, "name": "Cletus Jakuszewski" },
  { "id": 24, "extension": 2795, "name": "Ingemar Largen" },
  { "id": 25, "extension": 2020, "name": "Wheeler Seint" },
  { "id": 26, "extension": 6844, "name": "Melisande Mattaus" },
  { "id": 27, "extension": 5645, "name": "Andros Fatharly" },
  { "id": 28, "extension": 4697, "name": "Lurette Pellett" },
  { "id": 29, "extension": 1350, "name": "Cathryn Jeakins" },
  { "id": 30, "extension": 6936, "name": "Cori Shepley" },
  { "id": 31, "extension": 1766, "name": "Doralin Crafts" },
  { "id": 32, "extension": 3263, "name": "Sibella Dockwray" },
  { "id": 33, "extension": 6021, "name": "Basilio Cottle" },
  { "id": 34, "extension": 4551, "name": "Obie Turley" },
  { "id": 35, "extension": 4596, "name": "Yulma Yallowley" },
  { "id": 36, "extension": 2704, "name": "Tish Candlin" },
  { "id": 37, "extension": 2989, "name": "Roanna Cloake" },
  { "id": 38, "extension": 1853, "name": "Wilone Ebbing" },
  { "id": 39, "extension": 4367, "name": "Evangeline Benedite" },
  { "id": 40, "extension": 2621, "name": "Fremont Gilardoni" },
  { "id": 41, "extension": 6448, "name": "Anthony Izzat" },
  { "id": 42, "extension": 6989, "name": "Ferguson Gedney" },
  { "id": 43, "extension": 1829, "name": "Nydia Washington" },
  { "id": 44, "extension": 4274, "name": "Benton Bewsy" },
  { "id": 45, "extension": 4332, "name": "Lil Stork" },
  { "id": 46, "extension": 6853, "name": "Alfy Beevens" },
  { "id": 47, "extension": 5713, "name": "Julita Esh" },
  { "id": 48, "extension": 6608, "name": "Genny Fisbey" },
  { "id": 49, "extension": 1995, "name": "York Emeny" },
  { "id": 50, "extension": 6724, "name": "Jaime Rossborough" }])
const fields = ref([
  { key: 'extension', label: 'Extension', ordered: true },
  { key: 'name', label: 'Name', ordered: true },
  { key: 'action', label: 'Action', ordered: false }
])
</script>
