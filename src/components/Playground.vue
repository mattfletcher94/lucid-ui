<script setup lang="ts">
import '../styles/theme.css'
import { useAlert } from '../composables/useAlert'
import Button from './Button.vue'
import AlertProvider from './Alert/AlertProvider.vue'

const alert = useAlert({
  title: 'Oops, something went wrong!',
  message: 'Please try again later or contact support.',
  buttonLabel: 'Okay',
  variant: 'primary',
})

const onButtonClick = () => {
  alert.show().then(() => {
    console.log('Alert closed')
  })
}
</script>

<template>
  <AlertProvider teleport="body">
    <Button variant="primary" @click="onButtonClick">
      Primary Button
    </Button>
  </AlertProvider>
</template>
