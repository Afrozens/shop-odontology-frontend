<script lang="ts" setup>
defineProps<{
  isLoading: boolean;
  disabled?: boolean;
}>();
</script>

<template>
  <button
    :disabled="isLoading || disabled"
    class="btn-primary capitalize disabled:bg-gray-500 disabled:cursor-not-allowed disabled:opacity-80 text-text-footer text-minus-base btn-main"
  >
    <LoadingOutlined v-if="isLoading" />
    <slot v-else />
  </button>
</template>
