<script lang="ts" setup>
import { toRefs } from 'vue'
const props = defineProps({
  hue: {
    type: Number
  }
})

const { hue } = toRefs(props)
const saturationList = [0, 10, 20, 30, 40, 50, 60, 70, 80, 90, 100]
const lightnessList = [0, 10, 20, 30, 40, 50, 60, 70, 80, 90, 100]

function getHSLcolor(saturation: number, lightness: number): object {
  const style = {
    backgroundColor: `hsl(${hue.value}, ${saturation}%, ${lightness}%)`
  }
  return style
}

const styleTest = {
  backgroundColor: 'hsl(200,.5'
}
</script>

<template>
  <table class="color-table">
    <caption>Hue: {{ hue }}</caption>
    <thead>
      <tr>
        <th>
          lightness
          <br />/
          <br />saturation
        </th>
        <th v-for="saturation in saturationList" :key="saturation">{{ saturation }} %</th>
      </tr>
    </thead>
    <tbody>
      <tr class="color-table__line" v-for="lightness in lightnessList" :key="lightness">
        <th>{{ lightness }} %</th>
        <td v-for="saturation in saturationList" :key="saturation">
          <span class="color-table__block" :style="getHSLcolor(lightness, saturation)" />
        </td>
      </tr>
    </tbody>
  </table>
</template>

<style lang="postcss">
.color-table {
  caption {
    text-align: left;
    margin: 1em 0;
    font-weight: 700;
  }

  &__line {
    td {
      position: relative;
      padding: 0;
    }
  }

  &__block {
    position: absolute;
    display: block;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
  }
}
</style>
