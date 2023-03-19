---
title: Home
---
<script setup lang="ts">
import { h } from 'vue'
import '../../src/styles/theme.css'
import Button from '../../src/components/Button.vue'
import AlertProvider from '../../src/components/Alert/AlertProvider.vue'
import { useAlert } from '../../src/composables/useAlert'

const alert = useAlert({
  title: () => h('h1', 'Hello World!'),
  message: 'You clicked a button!',
  buttonLabel: 'OK',
});

const onButtonClick = () => {
  alert.show().then(() => {
    console.log('Alert closed');
  });
};

</script>
# My Vue Component Library

Here are some examples of using the `Button` component:

## Primary Button

<AlertProvider>
  <Button variant="primary" @click="onButtonClick">
    Primary Button
  </Button>
</AlertProvider>

## Secondary Button

<Button variant="secondary" @click="alert('Secondary button clicked!')">
  Secondary Button
</Button>

## Tertiary Button

<Button variant="tertiary" @click="alert('Tertiary button clicked!')">
  Tertiary Button
</Button>

## Button as Link

<Button tag="a" href="https://www.example.com" variant="primary">
  Visit Example.com
</Button>

## Button as Router Link

<Button tag="router-link" to="/guide" variant="primary">
  Go to Guide Page
</Button>
