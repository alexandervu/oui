<script lang="ts" setup>
// add slot which replace the default text value
import { ref, toRefs, PropType, onMounted, computed } from 'vue'

interface SwitchItem {
  title: string,
  value: string
}

const emit = defineEmits(['change'])
const props = defineProps({
  name: {
    type: String
  },
  items: {
    type: Array as PropType<SwitchItem[]>
  },
  checked: {
    type: String
  },
  align: {
    type: String,
    default: 'horizontal'
  },
  wrap: {
    type: Boolean,
    default: false
  }
})

let sliderElement = null
const { name, items, checked, align, wrap } = toRefs(props)
const radioValue = ref(checked?.value)

/**
 * Set main object css classes
 */
const classProps = computed(() => {
  const styleClasses = ['oui-switch']

  // horizontal or vertical alignment
  if (['horizontal', 'vertical'].includes(align.value)) {
    styleClasses.push(`oui-switch--${align.value}`)
  }

  // multiline
  if (wrap.value === true) {
    styleClasses.push('oui-switch--multiline')
  }

  return styleClasses.join(' ')
})

/**
 * When value change emit the the new value and re-set the slider.
 */
const valueChaged = (element) => {
  emit('change', radioValue.value)
  setSliderPosition(`switch-${name.value}-item-${element.target.dataset.index}`)
}

/**
 * When label size change cause of window or element resize, resize the slider.
 * To do so, find the checked radio element and resize the slider on his new shape.
 */
const elementResizeObserver = new ResizeObserver(entries => {
  sliderElement.classList.remove('slider--transition')
  const index = items.value.findIndex(element => element.value === radioValue.value)
  setSliderPosition(`switch-${name.value}-item-${index}`)
  sliderElement.classList.add('slider--transition')
})

/**
 * On mounting initialize the component by
 *   - getting slider element
 *   - find the index number of checked radio element
 *   - set the slider position and size on checked radio element label
 */
onMounted(() => {
  sliderElement = document.getElementById(`slider-${name.value}`)
  // find checked element and set slider
  const index = items.value.findIndex(element => element.value === checked.value)
  setSliderPosition(`switch-${name.value}-item-${index}`)
  // set resize observer
  items.value.forEach((_, index) => {
    const elementToObserve = document.getElementById(`switch-${name.value}-item-${index}`)
    elementResizeObserver.observe(elementToObserve)
  })
})

/**
 * Get the html label element throw it's id and set the slider to it's position and size.
 * @param {string} selectedElementId is the html label id of the corresponding radio input element.
 * @returns void
 */
function setSliderPosition(selectedElementId) {
  const selectedElement = document.getElementById(selectedElementId)
  if (sliderElement && selectedElement) {
    sliderElement.style.top = `${selectedElement.offsetTop}px`
    sliderElement.style.left = `${selectedElement.offsetLeft}px`
    sliderElement.style.height = `${selectedElement.offsetHeight}px`
    sliderElement.style.width = `${selectedElement.offsetWidth}px`
  }
}
</script>

<template>
  <div :className="classProps">
    <template v-for="(item, index) in items" :key="item.value">
      <input
        type="radio"
        :id="`switch-${name}-input-${index.toString()}`"
        :name="name"
        :value="item.value"
        :data-index="index.toString()"
        v-model="radioValue"
        @change="valueChaged"
      />
      <label
        :id="`switch-${name}-item-${index.toString()}`"
        :for="`switch-${name}-input-${index.toString()}`"
      >
        <span>{{ item.title }}</span>
      </label>
    </template>
    <span :id="`slider-${name}`" class="slider slider--transition"></span>
  </div>
</template>
