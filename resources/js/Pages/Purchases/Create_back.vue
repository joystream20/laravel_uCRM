<script setup>
import { getToday  } from '@/common'
import { onMounted, reactive, ref, computed } from 'vue'
import { Inertia } from '@inertiajs/inertia'

onMounted(() => {
form.date = getToday()

// console.log(props.items);
props.items.forEach( item => {
  itemList.value.push({
    id:item.id,
    name: item.name,
    price: item.price,
    quantity: 0
  })
})
})

const props = defineProps({
  'customers': Array,
  'items': Array
})

const itemList = ref([])

const form = reactive({
  date: null,
  customer_id: null,
  status : true,
  items: []
})

const quantity = ["0","1","2","3","4","5","6","7","8","9"]

const totalPrice = computed(() => {
  let total = 0;
  itemList.value.forEach( item => {
    total += item.price * item.quantity
  })
  return total
})

const storePurchase = () => {
  itemList.value.forEach( item => {
    if(item.quantity > 0){
      form.items.push({
        id: item.id,
        quantity: item.quantity
      })
    }
  })
  Inertia.post(route('purchases.store'), form)
}

</script>

<template>
  <div class="wrap p-10">
    <form @submit.prevent="storePurchase">
      Date<br>
      <input type="date" name="date" v-model="form.date">

      Member<br>
      <select name="customer" v-model="form.customer_id">
        <option v-for="customer in customers" :value="customer.id" :key="customer.id">
        {{customer.id}} : {{customer.name}}
        </option>
      </select>
      Product・Searvice<br>
      <table>
        <thead>
          <tr>
            <th>id</th>
            <th>商品名</th>
            <th>金額</th>
            <th class="px-4">数量</th>
            <th>金額</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in itemList">
          <td>{{ item.id }}</td>
          <td>{{ item.name }}</td>
          <td class="px-4">{{ item.price }}</td>
          <td class="p-2">
            <select name="quantity" v-model="item.quantity">
            <option v-for="q in quantity" :value="q">{{ q }}</option>
            </select>
          </td>
          <td>{{ item.price * item.quantity}}</td>
        </tr>
        </tbody>
    
      </table>
      <br>
      合計 {{ totalPrice }}円
      <button class=" text-white bg-indigo-500 border-0 py-2 px-6 mb-4">登録する</button>
    </form>
  </div>
</template>
