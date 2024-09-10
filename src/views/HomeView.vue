<template>
  <div class="w-full h-screen">
    <div
      class="flex justify-center bg-white px-10 py-32 sm:p-32 text-slate-800 dark:bg-green-300 dark:text-slate-900 h-full">
      <Tabs>
        <Tab title="First Tab">
          <div class="w-full h-full  p-2">
            <div class="w-full grid grid-cols-4 gap-4">
              <BasicInput :label="'label 1'" v-model="input1" error errorMessage="input Requerido" />
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
              <BasicInput :label="'label 1'" />
              <BasicInput :label="'label 1'" />
              <BasicInput :label="'label 1'" />
              <BasicInput :label="'label 1'" />
            </div>
          </div>
        </Tab>
        <Tab active title="Second Tab">
          <div class="w-full h-full p-2 flex justify-center items-center">
            hi?
          </div>
        </Tab>
        <Tab title="Third Tab">
          Third Tab content
        </Tab>
        <Tab title="Fourth Tab">
          Fourth Tab content
        </Tab>
        <Tab title="Fifth Tab">
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

const input1 = ref('')

const form = ref({
  sampleInputWithHelp: '',
  sampleInputWithError: '',
  sampleSuccessInput: '',
  sampleInfoInput: '',
  sampleWarningInput: '',
  sampleTextarea: '',
  sampleCheckbox: false,
  sampleSuccessCheckbox: true,
  sampleErrorCheckbox: false,
  sampleInfoCheckbox: true,
  sampleWarningCheckbox: false,
  sampleRadio: '',
  samplePreSelectedRadio: 'option2'
})
</script>
