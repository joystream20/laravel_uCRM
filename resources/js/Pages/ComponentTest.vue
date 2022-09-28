<script setup>
import GuestLayout from '@/Layouts/GuestLayout.vue'
import Label from '@/Components/InputLabel.vue'
import Input from '@/Components/TextInput.vue'
</script>

<template>
  <GuestLayout>
    <Label value="件名　">タイトル</Label>
    <Input modelValue="default words"></Input>
  </GuestLayout>
</template>
