<script setup>
  import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
  import { Head, Link } from '@inertiajs/inertia-vue3';
  import ValidationErrors from '@/Components/ValidationErrors.vue';
  import { reactive } from 'vue';
  import { Inertia } from '@inertiajs/inertia';



  defineProps({
    customer: Object
  });


  // const storeCustomer = () => {
  //   Inertia.post('/customers', form);
  // }

  const deleteItem = id => {
    Inertia.delete(route('customers.destroy', {customer: id}), {
      onBefore: () => {
        confirm('are you sure?');
      }
    })
  }

 
  </script>
  
  <template>
      <Head title="顧客登録" />
  
      <AuthenticatedLayout>
          <template #header>
              <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                  顧客登録
              </h2>
          </template>
  
          <div class="py-12">
              <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                  <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                      <div class="p-6 bg-white border-b border-gray-200">
                         
                        

                        <section class="text-gray-600 body-font relative">
                          <form @submit.prevent="storeCustomer">
                          <div class="container px-4 py-4 mx-auto">
                            
                            <div class="lg:w-1/2 md:w-2/3 mx-auto">
                              <div class="flex flex-wrap -m-2">
                                <div class="p-2  w-full mb-4">
                                  <div class="relative">
                                    <label for="name" class="leading-7 text-sm text-gray-600">顧客名</label>
                                    {{ customer.name }}
                                  </div>
                                </div>

                                <div class="p-2  w-full mb-4">
                                  <div class="relative">
                                    <label for="kana" class="leading-7 text-sm text-gray-600">顧客名ガナ</label>
                                    {{ customer.kana }}
                                  </div>
                                </div>

                                <div class="p-2  w-full mb-4">
                                  <div class="relative">
                                    <label for="tel" class="leading-7 text-sm text-gray-600">TEL</label>
                                    {{ customer.tel }}
                                  </div>
                                </div>

                                <div class="p-2  w-full mb-4">
                                  <div class="relative">
                                    <label for="email" class="leading-7 text-sm text-gray-600">Email</label>
                                    {{ customer.email }}
                                  </div>
                                </div>

                                <div class="p-2  w-full mb-4">
                                  <div class="relative">
                                    <label for="postcode" class="leading-7 text-sm text-gray-600">郵便番号</label>
                                    {{ customer.postcode }}
                                  </div>
                                </div>

                                <div class="p-2  w-full mb-4">
                                  <div class="relative">
                                    <label for="address" class="leading-7 text-sm text-gray-600">住所</label>
                                    {{ customer.address }}
                                  </div>
                                </div>

                                <div class="p-2  w-full mb-4">
                                  <div class="relative">
                                    <label for="birthday" class="leading-7 text-sm text-gray-600">誕生日</label>
                                    {{ customer.birthday }}
                                  </div>
                                </div>

                                <div class="p-2  w-full mb-4">
                                  <div class="relative flex">
                                    <label for="gender" class="leading-7 text-sm text-gray-600">性別</label>
                                    <div>
                                      <span v-if="customer.gender === 0">男</span>
                                      <span v-if="customer.gender === 1">女</span>
                                      <span v-if="customer.gender === 2">その他</span>
                                      
                                    </div>
                                  </div>
                                </div>
                                
                                <div class="p-2 w-full mb-4">
                                  <div class="relative">
                                    <label for="memo" class="leading-7 text-sm text-gray-600">メモ</label>
                                    {{ customer.memo }}
                                  </div>
                                </div>

                                

                                <div class="p-2 w-full">
                                  <div class="flex">
                                    <Link as="button" :href="route('customers.edit',
                                    {customer:customer.id})">
                                    <div class="flex mx-auto text-white bg-indigo-500 border-0 py-2 px-4 focus:outline-none hover:bg-indigo-600 rounded text-lg">編集する</div>
                                  </Link>

                                  <button @click="deleteItem(customer.id)" class="ml-2 bg-black text-white border-0 py-2 px-4 rouded text-lg">削除する</button>
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
