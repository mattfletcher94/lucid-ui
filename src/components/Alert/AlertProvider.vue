<script setup lang="ts">
import { computed } from 'vue'
import { alertsStore } from '../../stores/alerts'
import Alert from './Alert.vue'

const props = withDefaults(defineProps<{
  teleport?: string | HTMLElement
}>(), {
  teleport: 'body',
})

const alerts = computed(() => alertsStore.alerts.filter(alert => alert.show))
</script>

<template>
  <slot />
  <Teleport :to="props.teleport">
    <TransitionGroup
      name="alert-provider"
      tag="div"
      class="alert-provider"
    >
      <Alert
        v-for="(alert, index) in alerts"
        :id="alert.id"
        :key="index"
        :title="alert.title"
        :message="alert.message"
        :button-label="alert.buttonLabel"
        :variant="alert.variant"
      />
    </TransitionGroup>
  </Teleport>
</template>

<style>
.alert-provider {
  position: fixed;
  top: 0;
  left: 0;
  width: 0px;
  height: 0px;
  z-index: 9999;
  --alert-provider-transition-duration: 150ms;
}

.alert-provider-move, /* apply transition to moving elements */
.alert-provider-enter-active,
.alert-provider-leave-active {
  transition: all var(--alert-provider-transition-duration) ease;
}

.alert-provider-enter-from,
.alert-provider-leave-to {
  opacity: 0;
}

.alert-provider-move,
.alert-provider-enter-active .alert-card,
.alert-provider-leave-active .alert-card {
  transition: transform var(--alert-provider-transition-duration) ease;
}

.alert-provider-enter-from .alert-card {
  transform: scale(0.95);
}

.alert-provider-leave-to .alert-card {
  transform: scale(0.95);
}
</style>
