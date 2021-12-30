# Switch

The **switch** component is a simple customizable block.

| Prop    | Description                                                                                                                  | Accepted Values            | Default |
| :------ | :--------------------------------------------------------------------------------------------------------------------------- | :------------------------- | :------ |
| name    | Group name                                                                                                                   |                            |         |
| items   | Array of objects with `title` and `value` properties.                                                                        |                            |         |
| checked | String value matching one object value in `items` array.                                                                     |                            |         |
| align   | Alignment of items                                                                                                           | `horizontal` or `vertical` |         |
| wrap    | Sets whether items are forced onto one line or can wrap onto multiple lines. Wrap has only effect on `horizontal` alignment. | `true` or `false`          |         |

```vue
  <h3>Horizontal - no wrap</h3>
  <OuiSwitch name="HnoWrapSwitch" :items="items" :checked="items[1].value" />

  <h3>Horizontal - wrap</h3>
  <OuiSwitch name="HWrapSwitch" :items="items" :checked="items[0].value" :wrap="true" />

  <h3>Vertical</h3>
  <OuiSwitch name="VSwitch" :items="items" :checked="items[0].value" align="vertical" />
```

<SwitchExample />

<script setup>
import SwitchExample from './SwitchExample.vue'
</script>
