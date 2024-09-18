<template>
    <div v-show="isActive">
      <slot></slot>
    </div>
  </template>
  
  <script setup>
  import { inject, onMounted, ref, computed } from 'vue'
  import { useAttrs } from 'vue'
  
  // Consumir los tabs proporcionados por el componente padre
  const tabs = inject('tabs')
  
  // Atributos recibidos por props
  const attrs = useAttrs()
  const name = attrs.name
  const selected = attrs.selected || false
  
  // Variable reactiva para controlar si la tab está activa
  const isActive = ref(false)
  
  // Computed para generar el href
  const href = computed(() => `#${name.toLowerCase().replace(/ /g, '-')}`)
  
  console.log(href.value)
  // Agregar la tab a la lista de tabs y establecer si está seleccionada
  onMounted(() => {
    tabs.push({
      name,
      href: href.value,
      isActive: isActive.value = selected
    })
  })
  </script>
  