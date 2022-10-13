<script setup>
  import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
  import { Head, Link } from '@inertiajs/inertia-vue3';
  import ValidationErrors from '@/Components/ValidationErrors.vue';
  import { onMounted, reactive, ref, computed } from 'vue'
  import { Inertia } from '@inertiajs/inertia';
  import FormValidationErrors from '@/Components/ValidationErrors.vue';
  import dayjs from 'dayjs';


  onMounted(() => {
    console.log(props.items)
    console.log(props.order)
    //console.log(props.order[0].customer_name)

})

const props = defineProps({
  // 'customers': Array,
  'items': Array,
  'order' : Array

})



  </script>
  
  <template>
      <Head title="購買履歴 詳細画面" />
  
    <AuthenticatedLayout>
      <template #header>
          <h2 class="font-semibold text-xl text-gray-800 leading-tight">
              購買履歴 詳細画面
          </h2>
      </template>

      <div class="py-12">
        <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
          <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
            <div class="p-6 bg-white border-b border-gray-200">
                
              <FormValidationErrors class="mb-4" />

              <section class="text-gray-600 body-font relative">
                <form @submit.prevent="storePurchase">
                <div class="container px-4 py-4 mx-auto">
                  
                <div class="lg:w-1/2 md:w-2/3 mx-auto">
                  <div class="flex flex-wrap -m-2">

                  <div class="p-2  w-full">
                    <div class="relative">
                      <label for="date" class="leading-7 text-sm text-gray-600">Date</label>
                      <div name="date" class="w-full bg-gray-100 bg-opacity-50 rounded border border-gray-300 focus:border-indigo-500 focus:bg-white focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out">
                        {{ dayjs(props.order[0].created_at).format('YYYY-MM-DD HH:mm:ss') }}</div>

                    </div>
                  </div>
                    
                  <div class="p-2 w-full">
                    <div class="relative">
                      
                      <label for="customer" class="leading-7 text-sm text-gray-600">Member</label>
                      <p class="w-full bg-gray-100 bg-opacity-50 rounded border border-gray-300 focus:border-indigo-500 focus:bg-white focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out">{{ props.order[0].customer_name}}</p>
                    </div>
                  </div>

                  <div class="p-2 w-full mx-auto overflow-auto">
                    <table class="w-full">
                      <thead class="w-full bg-gray-100 bg-opacity-50 rounded border border-gray-300 focus:border-indigo-500 focus:bg-white focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out">
                        <tr>
                          <th class="py-2 px-4">id</th>
                          <th class="py-2 px-4">商品名</th>
                          <th class="py-2 px-4">金額</th>
                          <th class="py-2 px-4">数量</th>
                          <th class="py-2 px-4">小計</th>
                        </tr>
                      </thead>
                      <tbody>
                        <tr v-for="item in props.items">
                        <td class="p-4">{{ item.item_id }}</td>
                        <td class="p-4">{{ item.item_name }}</td>
                        <td class="p-4">{{ item.item_price }}</td>
                        <td class="p-4">{{ item.quantity }}</td>
                        <td>{{ item.subtotal}}</td>
                      </tr>
                      </tbody>
                  
                    </table>
                    
                  </div>

                    <div class="p-2 w-full">
                      <div class="w-full bg-gray-100 bg-opacity-50 rounded border border-gray-300 focus:border-indigo-500 focus:bg-white focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out">
                        合計 {{ props.order[0].total }}円
                      </div>
                    </div>

                    
                    
                    <div class="p-2 w-full">
                      <div class="">
                        <label class="leading-7 text-sm text-gray-600">ステータス</label>
                        <div v-if="props.order[0].status == true" class="w-full bg-gray-100 bg-opacity-50 rounded border border-gray-300 focus:border-indigo-500 focus:bg-white focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out">
                          未キャンセル
                        </div>
                        <div v-if="props.order[0].status == false" class="w-full bg-gray-100 bg-opacity-50 rounded border border-gray-300 focus:border-indigo-500 focus:bg-white focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out">
                          キャンセル済
                        </div>
                      </div>
                    </div>

                    <div class="p-2 w-full">
                      <label class="leading-7 text-sm text-gray-600">キャンセル日</label>
                      <div v-if="props.order[0].status == false" class="w-full bg-gray-100 bg-opacity-50 rounded border border-gray-300 focus:border-indigo-500 focus:bg-white focus:ring-2 focus:ring-indigo-200 text-base outline-none text-gray-700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out">
                        {{ dayjs(props.order[0].updated_at).format('YYYY-MM-DD HH:mm:ss') }}
                      </div>
                    </div>
                    
                    <div v-if="props.order[0].status == true" class="p-2 w-full">
                      <div class="">
                        <Link as="button" :href="route('purchases.edit',{purchase: props.order[0].id})" class="flex mx-auto text-white bg-indigo-500 border-0 py-2 px-6">編集する</Link>
                        
                      </div>
                    </div>
                    
                  </div>
                </div>
                </div>
              </form>
              </section>
            </div>
          </div>
        </div>
      </div>
    </AuthenticatedLayout>
  </template>
  
  <style>
    .flex-wrap{
      flex-wrap:wrap;
    }
  </style>
