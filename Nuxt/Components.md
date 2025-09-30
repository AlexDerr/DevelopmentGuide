# Nuxt Components

## Naming

## Props

Props are how data is passed from the parent to the component. These are technically not mutable, although if the prop is an object its properties can be changed and those changes would be reflected in the parent. Generally, the `modelValue` prop should be used for "mutating" a prop, which automatically handles creating the emit event when that prop changes, so the parent can get the updated value. This only works for the `modelValue` prop, and would have to be manually setup for any others. When using `modelValue`, the parent will pass the value with `v-model`. All other props will be passed with `:prop-name`

### Simple Props

```typescript
// ~/components/my-component.vue

<script setup lang="ts">
const props = defineProps({
    modelValue: {
        type: string,
        required: true,
    },
    myProp: {
        type: string,
        required: true,
    },
    optionalProp: {
        type: number,
        required: false,
        default: 0,
    },

});
</script>
```

```html
<!-- ~/pages/index.vue -->

<!-- Usage of my-component.vue with default optionalProp value-->
<MyComponent v-model="myModelValue" :my-prop="myPropValue"/>

<!-- Usage of my-component.vue with passed optionalProp value-->
<MyComponent v-model="myModelValue" :my-prop="myPropValue" :optional-prop="optionalValue" />
```

### Prop Typing

Vue does not allow props to be typed directly as a class or interface you have defined yourself if you want to do typechecking with tools like `vue-tsc`. They can be typed instead by using `PropType`.

```typescript
<script setup lang="ts">
import type { PropType } from "vue";

const props = defineProps({
    modelValue: {
        type: Object as PropType<myType>,
        required: true,
    },
});
</script>
```

## Emits

## Slots