<template>
  <div class="w-full h-screen">
    <div
      class="flex justify-center bg-white px-10 py-32 sm:p-32 text-slate-800 dark:bg-green-300 dark:text-slate-900 h-full">
      <Tabs>
        <Tab active title="First Tab">
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
              <Switch :label="'label 1'" />
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
        <Tab title="Second Tab">
          <div class="w-full h-full p-2 flex justify-center items-center">
            <PasswordInput label="Password" error errorMessage="input Requerido" placeholder="e.g" />
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
import PasswordInput from '@/components/UiComponents/InputsComponents/PasswordInput.vue';
import Switch from '@/components/UiComponents/Toggles/Switch.vue';

const input1 = ref('')

const error = true
</script>
