<script setup>

</script>

<template>
  <div v-if="$page.props.flash.status === 'success'" class="bg-blue-500 text-white px-4 py-4 mb-4">{{ $page.props.flash.message }}</div>
  <div v-if="$page.props.flash.status === 'danger'" class="bg-red-500 text-white px-4 py-4 mb-4">{{ $page.props.flash.message }}</div>
</template>
