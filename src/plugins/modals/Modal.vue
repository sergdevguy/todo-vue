<script setup>
  import { computed, inject } from 'vue'

  const
    $props = defineProps({
      name: { type: String, default: "" },
      title: { type: String, default: "Модальный диалог" }
    }),
    $modals = inject("$modals"),
    _show = computed(() => {
      return $modals.active() == $props.name
    })

  function closeModal(accept = false) {
    accept ? $modals.accept() : $modals.cancel()
  }
</script>

<template>
  <div class="viewport-wrapper" v-if="_show">
    <div class="dialog-wrapper">
      <header>{{ $props.title }}</header>
      <main>
        <slot></slot>
      </main>
      <footer>
        <button @click="closeModal(true)">Accept</button>
        <button @click="closeModal(false)">Cancel</button>
      </footer>
    </div>
  </div>
</template>