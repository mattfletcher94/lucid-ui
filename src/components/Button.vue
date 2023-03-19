<script setup lang="ts">
const props = withDefaults(defineProps<{
  tag?: 'button' | 'a' | 'router-link'
  variant?: 'primary' | 'secondary' | 'tertiary' | 'success' | 'danger' | 'warning' | 'dark' | 'light'
  href?: string
  to?: string
  type?: 'button' | 'submit' | 'reset'
  label?: string
  block?: boolean
}>(), {
  tag: 'button',
  variant: 'primary',
  type: 'button',
  block: false,
})
</script>

<template>
  <component
    :is="tag"
    class="lucid-btn"
    :class="{
      'lucid-btn--primary': props.variant === 'primary',
      'lucid-btn--secondary': props.variant === 'secondary',
      'lucid-btn--tertiary': props.variant === 'tertiary',
      'lucid-btn--success': props.variant === 'success',
      'lucid-btn--danger': props.variant === 'danger',
      'lucid-btn--warning': props.variant === 'warning',
      'lucid-btn--dark': props.variant === 'dark',
      'lucid-btn--light': props.variant === 'light',
      'lucid-btn--block': props.block,
    }"
    :href="props.tag === 'a' ? props.href : undefined"
    :to="props.tag === 'router-link' ? props.to : undefined"
    :type="props.tag === 'button' ? props.type : undefined"
  >
    <slot />
  </component>
</template>

<style scoped>
.lucid-btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  font-size: 0.875rem;
  padding: 0.5rem 1rem;
  border-radius: 0.375rem;
  font-weight: 600;
  transition-property: all;
  transition-duration: 0.2s;
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
  text-decoration: none;
  cursor: pointer;
  outline: 2px solid transparent;
  outline-offset: 0.125rem;
}

.lucid-btn.lucid-btn--block {
  display: flex;
  width: 100%;
}

.lucid-btn--lg {
  padding: 0.75rem 2.5rem;
}

.lucid-btn--sm {
  padding: 0.375rem 1rem;
  font-size: 0.875rem;
}

.lucid-btn.lucid-btn--primary {
  background-color: var(--lucid-color-primary);
  color: var(--lucid-color-primary-contrast);
}

.lucid-btn.lucid-btn--primary:hover,
.lucid-btn.lucid-btn--primary:active {
  background-color: var(--lucid-color-primary-shade);
}

.lucid-btn.lucid-btn--primary:focus-within {
  outline-color: var(--lucid-color-primary);
}

.lucid-btn.lucid-btn--secondary {
  background-color: var(--lucid-color-secondary);
  color: var(--lucid-color-secondary-contrast);
}

.lucid-btn.lucid-btn--secondary:hover,
.lucid-btn.lucid-btn--secondary:active {
  background-color: var(--lucid-color-secondary-shade);
}

.lucid-btn.lucid-btn--secondary:focus-within {
  outline-color: var(--lucid-color-secondary);
}

.lucid-btn.lucid-btn--tertiary {
  background-color: var(--lucid-color-tertiary);
  color: var(--lucid-color-tertiary-contrast);
}

.lucid-btn.lucid-btn--tertiary:hover,
.lucid-btn.lucid-btn--tertiary:active {
  background-color: var(--lucid-color-tertiary-shade);
}

.lucid-btn.lucid-btn--tertiary:focus-within {
  outline-color: var(--lucid-color-tertiary);
}

.lucid-btn.lucid-btn--success {
  background-color: var(--lucid-color-success);
  color: var(--lucid-color-success-contrast);
}

.lucid-btn.lucid-btn--success:hover,
.lucid-btn.lucid-btn--success:active {
  background-color: var(--lucid-color-success-shade);
}

.lucid-btn.lucid-btn--success:focus-within {
  outline-color: var(--lucid-color-success);
}

.lucid-btn.lucid-btn--danger {
  background-color: var(--lucid-color-danger);
  color: var(--lucid-color-danger-contrast);
}

.lucid-btn.lucid-btn--danger:hover,
.lucid-btn.lucid-btn--danger:active {
  background-color: var(--lucid-color-danger-shade);
}

.lucid-btn.lucid-btn--danger:focus-within {
  outline-color: var(--lucid-color-danger);
}

.lucid-btn.lucid-btn--warning {
  background-color: var(--lucid-color-warning);
  color: var(--lucid-color-warning-contrast);
}

.lucid-btn.lucid-btn--warning:hover,
.lucid-btn.lucid-btn--warning:active {
  background-color: var(--lucid-color-warning-shade);
}

.lucid-btn.lucid-btn--warning:focus-within {
  outline-color: var(--lucid-color-warning);
}

.lucid-btn.lucid-btn--dark {
  background-color: var(--lucid-color-dark);
  color: var(--lucid-color-dark-contrast);
}

.lucid-btn.lucid-btn--dark:hover,
.lucid-btn.lucid-btn--dark:active {
  background-color: var(--lucid-color-dark-shade);
}

.lucid-btn.lucid-btn--dark:focus-within {
  outline-color: var(--lucid-color-dark);
}

.lucid-btn.lucid-btn--light {
  background-color: var(--lucid-color-light);
  color: var(--lucid-color-light-contrast);
}

.lucid-btn.lucid-btn--light:hover,
.lucid-btn.lucid-btn--light:active {
  background-color: var(--lucid-color-light-shade);
}

.lucid-btn.lucid-btn--light:focus-within {
  outline-color: var(--lucid-color-light);
}
</style>
