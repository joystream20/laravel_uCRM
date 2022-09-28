<script setup>
  import { Inertia } from '@inertiajs/inertia';

defineProps ({
id : String,
blog: Object
});

const deleteConfirm = id => {
  Inertia.delete(`/inertia/${id}`, {
    onBefore: () => confirm('削除します？')
  })
}
</script>

<template>
  {{ id }}<br>
  {{  blog.title }}<br>
  <button @click="deleteConfirm(blog.id)">delete</button>
</template>
