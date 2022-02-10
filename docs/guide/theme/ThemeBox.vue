<template>
  <div class="oui-theme theme-box">
    <header>
      <h3>Scheme</h3>
      <form id="theme-switcher">
        <OuiSwitch
          name="theme"
          align="horizontal"
          :items="themeItems"
          :checked="selection"
          @change="onChange"
        />
      </form>
    </header>
    <slot></slot>
  </div>
</template>
<script lang="ts" setup>
import { ref, onMounted } from 'vue'
import { OuiSwitch } from '../../../src/oui.esm.ts'

let doc = null
const selection = ref('light')
const themeItems = ref([
  {
    title: 'Light',
    value: 'light'
  },
  {
    title: 'Dark',
    value: 'dark'
  },
  {
    title: 'Dim',
    value: 'dim'
  }
])

onMounted(() => {
  doc = document.firstElementChild
  selection.value = doc?.getAttribute('color-scheme') || 'light'
})

function onChange(value) {
  console.log(':::', value)
  doc.setAttribute('color-scheme', value)
}  
</script>
<style lang="postcss">
.theme-box {
  padding: 1rem;
  border-radius: 5px;
}

.theme-box header {
  display: inline-grid;
  gap: 1ch;
  margin-bottom: 2ch;
  text-align: center;
  width: 100%;
}

.theme-box header h3 {
  margin-top: 0;
}

.theme-box form {
  display: flex;
  gap: 2ch;
  justify-content: center;

  & > div {
    display: inline-flex;
    align-items: center;
    gap: 0.75ch;
  }
}

.theme-box section {
  display: grid;
  gap: 2.5vh;
}
</style>
