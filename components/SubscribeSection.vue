<template>
   <section id="subscribe">
      <div
         class="absolute z-0 w-screen h-56 py-56 m-auto opacity-75 xl:py-64 bg-black-mimi"
      ></div>
      <div class="z-10 h-16"></div>
      <div class="z-10 flex flex-row items-center justify-around">
         <img
            class="z-10 hidden mr-20 opacity-100 lg:w-3/12 md:w-3/12 md:mr-10 md:block"
            src="/svg/newsletter.min.svg"
            alt=""
         />
         <div
            class="relative z-10 flex flex-col items-center justify-center w-64 h-auto"
         >
            <h1 class="text-4xl text-center text-white font-primary">
               Newsletter
            </h1>
            <p
               id="description"
               class="mt-4 text-base text-center text-white font-secondary"
            >
               {{ $t('subscribeSection.description') }}
            </p>
            <input
               v-model="email"
               class="w-64 h-10 p-4 mt-6 rounded shadow-xl focus:outline-none font-secondary"
               type="text"
               :placeholder="$t('subscribeSection.inputPlaceholder')"
               aria-label="email"
            />
            <div v-if="subscribeSucceed">
               <p
                  class="mt-4 text-xs italic text-center text-green-400 font-secondary"
               >
                  {{ $t('subscribeSection.successMessage') }}
               </p>
            </div>
            <p
               class="mt-4 text-xs italic text-center text-white font-secondary"
            >
               {{ $t('subscribeSection.unsubscribe') }}
            </p>
            <div class="flex items-baseline justify-center w-screen">
               <p
                  class="mt-4 text-xs italic text-center text-white font-secondary"
               >
                  {{ $t('subscribeSection.terms') }}
                  <input class="pt-px ml-3" type="checkbox" />
               </p>
            </div>

            <button
               class="w-40 h-10 mt-6 font-semibold tracking-wider text-white uppercase rounded shadow-sm focus:outline-none focus:underline bg-violet-mimi hover:bg-orange-mimi"
               @click="subscribe()"
            >
               {{ $t('subscribeSection.button') }}
            </button>
         </div>
         <img
            class="z-10 hidden ml-20 lg:w-3/12 md:w-3/12 md:ml-10 md:block"
            src="/svg/newsletterStart.min.svg"
            alt=""
         />
      </div>
   </section>
</template>

<script>
import axios from 'axios';
export default {
   data() {
      return {
         email: '',
         subscribeSucceed: false
      };
   },
   methods: {
      async subscribe() {
         const response = await axios.post('/.netlify/functions/subscribe', {
            email: this.email
         });
         const { errors } = response;

         if (errors) {
            alert(errors);
         }
         this.subscribeSucceed = true;
         setTimeout(() => {
            this.email = '';
            this.subscribeSucceed = false;
         }, 6000);
      }
   }
};
</script>

<style></style>
