<template>
  <div class="w-full h-screen">
    <div
      class="flex items-center justify-center bg-white p-16 text-slate-800 dark:bg-cyan-900 dark:text-slate-900 h-full">
      <div class="flex h-96 w-full flex-col rounded-lg bg-white border border-slate-300 dark:border-slate-600">
        <!-- modo pantalla pequeña -->
        <div class="block px-2 pt-3 sm:hidden">
          <button @click="toggleDropdown"
            class="relative flex w-full items-center justify-between rounded-md border border-slate-300 bg-white p-2 capitalize dark:border-slate-600 dark:bg-slate-800">
            {{ currentSection }}
            <ChevronDownIcon class="h-5 w-5 transition-transform" :class="isDropdownOpen ? 'rotate-180' : 'rotate-0'" />
            <div v-show="isDropdownOpen"
              class="absolute left-0 top-12 z-10 w-full rounded-md border border-slate-300 bg-white shadow-md dark:border-slate-600 dark:bg-slate-800">
              <div v-for="section in sections" :key="section" @click="selectSection(section)"
                class="cursor-pointer px-4 py-2 hover:bg-slate-200 dark:hover:bg-slate-700">
                {{ section.charAt(0).toUpperCase() + section.slice(1) }}
              </div>
            </div>
          </button>
        </div>
        <!-- modo pantalla pequeña -->
        <!-- Header Section -->
        <div
          class="relative hidden w-full gap-4 border-b border-slate-300 px-2 pt-3 sm:flex md:px-5 dark:border-slate-600">
          <div class="absolute bottom-0 left-0 h-0.5 bg-indigo-500 transition-transform duration-500" :style="{
            width: underlineWidth + 'px',
            transform: 'translateX(' + underlineOffset + 'px)',
          }"></div>
          <div v-for="(section, index) in sections" :key="index" ref="tabHeader" @click="setSection(section)"
            class="pb-2 text-center md:min-w-24" :class="tabClass(section)">
            {{ section.charAt(0).toUpperCase() + section.slice(1) }}
          </div>
          <!-- <div ref="notificationsRef" @click="setSection('notifications')" class="pb-2 text-center md:min-w-24"
            :class="tabClass('notifications')">
            Notifications
          </div>
          <div ref="securityRef" @click="setSection('security')" class="pb-2 text-center md:min-w-24"
            :class="tabClass('security')">
            Security
          </div> -->
        </div>
        <!-- header section -->
        <!-- panel section -->
        <div class="h-full">
          <div class="flex h-full w-full items-center justify-center" v-if="currentSection === 'profile'">
            Profile Settings
          </div>
          <div class="w-full flex h-full items-center justify-center" v-else-if="currentSection === 'notifications'">
            Notifications Settings
          </div>
          <div class="w/full flex h-full items-center justify-center" v-else-if="currentSection === 'security'">
            Security Settings
          </div>
        </div>
        <!-- panel section -->
      </div>
    </div>
  </div>

</template>

<script setup>
import Tabs from "@/components/UiComponents/Tabs/Tabs.vue";
import { ref, onMounted } from "vue";
// import { ChevronDownIcon } from "@heroicons/vue/24/outline";

const sections = ["profile", "notifications", "security"];
const currentSection = ref("profile");
const isDropdownOpen = ref(false);

const tabHeader = ref(null);

const profileRef = ref(null);
const notificationsRef = ref(null);
const securityRef = ref(null);

const underlineWidth = ref(0);
const underlineOffset = ref(0);

const toggleDropdown = () => {
  isDropdownOpen.value = !isDropdownOpen.value;
};

const selectSection = (section) => {
  currentSection.value = section;
  updateUnderlinePosition();
};

const setSection = (section) => {
  currentSection.value = section;
  updateUnderlinePosition();
};

const tabClass = (section) => {
  return currentSection.value !== section
    ? "cursor-pointer border-b border-transparent hover:border-slate-300 dark:hover:border-slate-600"
    : "bg-gray-200";
};

const updateUnderlinePosition = () => {
  let targetRef = null;

  targetRef = tabHeader.value[sections.indexOf(currentSection.value)];
  // switch (section) {
  //   case "profile":
  //     targetRef = profileRef.value;
  //     break;
  //   case "notifications":
  //     targetRef = notificationsRef.value;
  //     break;
  //   case "security":
  //     targetRef = securityRef.value;
  //     break;
  // }
  console.log(targetRef)

  if (targetRef) {
    underlineWidth.value = targetRef.offsetWidth;
    underlineOffset.value = targetRef.offsetLeft;
  }
};

onMounted(() => {
  updateUnderlinePosition(currentSection.value);
});
</script>