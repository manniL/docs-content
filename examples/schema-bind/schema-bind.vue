<template>
  <FormKitSchema :schema="schema" :data="data" />
</template>

<script setup>
import { reactive } from 'vue'

const schema = [
  {
    $el: 'h1',
    // 👀 Look below for the data object with this
    bind: '$someAttributes',
    children: 'Click me!',
  },
]

const data = reactive({
  someAttributes: {
    class: 'red',
    onClick: () => {
      if (data.someAttributes.class === 'red') {
        data.someAttributes.class = 'blue'
      } else {
        data.someAttributes.class = 'red'
      }
    },
    'data-fruit': 'I like fruit',
  },
})
</script>

<style>
.red {
  color: red;
}
.blue {
  color: blue;
}
</style>
