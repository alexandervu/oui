<script setup>
import { ref } from 'vue'
import { OuiSwitch } from '../../../src/oui.esm.ts'
import ThemeBox from '../theme/ThemeBox.vue'

const items = ref([
  {
    title: 'Title 1',
    value: 'Value 1'
  },
  {
    title: 'Title 2',
    value: 'Value 2'
  },
  {
    title: 'Title 3',
    value: 'Value 3'
  },
  {
    title: 'Title 4',
    value: 'Value 4'
  },
  {
    title: 'Title 5',
    value: 'Value 5'
  }
])
</script>

<template>
  <ThemeBox>
    <section>
      <h3>Horizontal - no wrap</h3>
      <OuiSwitch name="HnoWrapSwitch" :items="items" :checked="items[1].value" />
      <h3>Horizontal - wrap</h3>
      <OuiSwitch name="HWrapSwitch" :items="items" :checked="items[0].value" :wrap="true" />
      <h3>Vertical</h3>
      <OuiSwitch name="VSwitch" :items="items" :checked="items[0].value" align="vertical" />
    </section>
  </ThemeBox>
</template>
