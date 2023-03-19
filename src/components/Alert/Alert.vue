<script setup lang="ts">
import type { VNode } from 'vue'
import { ref } from 'vue'
import { useFocusTrap } from '@vueuse/integrations/useFocusTrap'
import { useRenderOrProp } from '../../composables/useRenderOrProp'
import Button from '../Button.vue'
import type { variants } from '../../types'
import { alertsStore } from '../../stores/alerts'

const props = defineProps<{
  id: string
  title: string | (() => VNode)
  message: string | (() => VNode)
  buttonLabel: string | (() => VNode)
  variant: variants
}>()

const target = ref()

const { component: titleComponent } = useRenderOrProp(props.title)
const { component: messageComponent } = useRenderOrProp(props.message)
const { component: labelComponent } = useRenderOrProp(props.buttonLabel)

useFocusTrap(target, { immediate: true })

const hide = () => {
  alertsStore.close(props.id)
}
</script>

<template>
  <div
    ref="target"
    class="alert"
    role="alertdialog"
    :aria-labelledby="`alert-title-${props.id}`"
    :aria-describedby="props.message ? `alert-message-${props.id}` : undefined"
    tabindex="0"
    @keydown.esc="hide"
  >
    <button
      type="button"
      title="Close alert"
      aria-hidden="true"
      aria-label="Close alert"
      class="alert-backdrop"
      tabindex="-1"
      @click="hide"
    />
    <div
      ref="target"
      class="alert-card"
    >
      <h2
        :id="`alert-title-${props.id}`"
        class="alert-card__title"
      >
        <titleComponent />
      </h2>
      <div
        v-if="props.message"
        :id="`alert-message-${props.id}`"
        class="alert-card__message"
      >
        <messageComponent />
      </div>
      <div
        class="alert-card__button-wrapper"
      >
        <Button
          class="alert-card__button"
          aria-label="Close alert"
          title="Close alert"
          :variant="props.variant"
          @click="hide"
        >
          <labelComponent />
        </Button>
      </div>

    </div>
  </div>
</template>

<style>
.alert {
  display: flex;
  overflow: hidden;
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  padding: 2rem;
  justify-content: center;
  align-items: center;
  height: 100%;
  width: 100%;
  z-index: 999;
}

.alert .alert-backdrop {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background-color: #1e293b;
  opacity: 0.7;
  cursor: default;
}

.alert-card {
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: start;
  align-items: start;
  gap: 0.5rem;
  width: 100%;
  max-width: 350px;
  padding: 1.5rem;
  background-color: #ffffff;
  border-radius: 0.375rem;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
}

.alert-card__title {
  display: block;
  width: 100%;
  text-align: left;
  color: #111827;
  font-size: 1.25rem;
  line-height: 1.75rem;
  font-weight: 600;
}

.alert-card__message {
  display: block;
  width: 100%;
  text-align: left;
  color: #374151;
  font-size: 1rem;
  line-height: 1.25rem;
  font-weight: 400;
}

.alert-card__button-wrapper {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  width: 100%;
}

.alert-card__button {
  margin-top: 1rem;
  min-width: 90px;
}
</style>
