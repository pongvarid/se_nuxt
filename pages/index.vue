<template>
<div>
    <section class="bg-white py-8">
        <div class="container mx-auto flex items-center flex-wrap pt-4 pb-12">
            <nav id="store" class="w-full z-30 top-0 px-6 py-1">
                <div class="w-full container mx-auto flex flex-wrap items-center justify-between mt-0 px-2 py-3">
                    <a class="uppercase tracking-wide no-underline hover:no-underline font-bold text-gray-800 text-xl" href="#">
                        Store
                    </a>

                    <div class="flex items-center" id="store-nav-content">

                       <button @click="cartState = !cartState" class="pl-3  flex" href="#">
                            <svg class="fill-current hover:text-black" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24">
                                <path d="M7 11H17V13H7zM4 7H20V9H4zM10 15H14V17H10z" />
                            </svg>
                            ชำระเงิน
                        </button>
                            <div  class="fixed bottom-6 shadow-xl flex bg-yellow-400 rounded-full p-4 "><img class="w-6 h-6" src="https://cdn.iconscout.com/icon/free/png-256/shopping-cart-452-1163339.png" alt=""> {{chooseProducts.length}} </div>
                     
                    </div>
                </div>
            </nav>

            <div class="w-full" v-if="cartState">
              <Price :products="chooseProducts" />
            </div>
       

            <div v-else class="w-full md:w-1/3 xl:w-1/4 p-6 flex flex-col" v-for="product,i in products" :key="i">
                <a href="#">
                    <img class="hover:grow hover:shadow-lg h-48" :src="product.image" />
                    <div class="pt-3 flex items-center justify-between">
                        <div>
                            <p class="text-xl font-bold">{{product.name}}</p>
                        </div>
                    </div>
                    <p class="text-yellow-600 font-bold">$ {{product.price}} </p>
                    <form class="flex  " @submit.prevent="addProduct(product)" :ref="'product_'+product.id" >
                        <input required v-model="product.count" value="1" class="w-2/3 border-2 border-blue-200" type="text" placeholder="จำนวน">
                        <button type="submit" class="w-1/3 rounded-xl bg-green-600 text-white"> เพิ่ม </button>
                    </form>
                </a>
            </div>

        </div>
    </section>
</div>
</template>

<script>
import products from '@/static/products.json'
import _ from 'lodash'
export default {
    data: () => {
        return {
            products: products,
            chooseProducts: [],
            cartState: false,
        };
    },
    methods: {

        async addProduct(product) {
            if (this.checkProduct(product)) {
                this.chooseProducts.push(product);
            } else {
                alert('เลือกสินค้านี้แล้ว');
            } 
        },
        checkProduct(product) {
            let check = _.filter(this.chooseProducts, { id: product.id })
            return (check.length > 0) ? false : true

        }

    },
    async created() {

    },
};
</script>

<style>
</style>
