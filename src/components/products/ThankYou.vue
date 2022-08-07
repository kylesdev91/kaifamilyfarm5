<template>
  <div class="backdrop" @click="closeThankYou">
    <div class="modal" :class="{ sale: theme === 'sale' }">
      <Spinner  v-if="showSpinner"/>
      <h1 class="thanks" v-if="showThankYou">{{ thankYouMessage }}</h1>
      
    </div>
  </div>
</template>

<script>
import Spinner from '@/components/products/Spinner.vue'
export default {
  props: ['responseFromCart'],
  components: {
    Spinner
  },
  data() {
    return {
      showSpinner: false,
      showThankYou: false,
      // responseFromCart: 200,
      thankYouMessage: 'Thank You!'
    }
  },
  methods: {
    closeThankYou() {
      this.$emit('close');
    },
  },
   async mounted() {
    console.log('The response status from CART.vue is ' + this.responseFromCart)
      if(this.responseFromCart !== 200){
        this.thankYouMessage = 'Error!'
      }

      this.showSpinner = true;
      await new Promise(resolve => {
        setTimeout(resolve, 2000)
      })
      this.showSpinner = false;
      this.showThankYou = true;
      }
  }
</script>

<style>
.modal {
  width: 200px;
  padding: 10px;
  margin: 200px auto;
  background: white;
  border-radius: 10px;
}
.backdrop {
  top: 0;
  position: fixed;
  background: rgba(0, 0, 0, 0.5);
  width: 100%;
  height: 100%;
}
.modal h1 {
  color: black;
  border: none;
  padding: 0;
  font-size: 30px;
  text-align: center;
}
.modal p {
  font-style: normal;
}


/* sale styles */
.modal.sale {
  background: green;
  color: white;
}
.modal.sale h1 {
  color: white;
}
</style>
