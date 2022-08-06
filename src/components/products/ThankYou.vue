<template>
  <div class="backdrop" @click="closeThankYou">
    <div class="modal" :class="{ sale: theme === 'sale' }">
      <Spinner  v-if="showSpinner"/>
      <h1 class="thanks" v-if="showThankYou">Thank you!</h1>
    </div>
  </div>
</template>

<script>
import Spinner from '@/components/products/Spinner.vue'
export default {
  components: {
    Spinner
  },
  data() {
    return {
      showSpinner: false,
      showThankYou: false
    }
  },
  methods: {
    closeThankYou() {
      this.$emit('close');
    },
  },
   async mounted() {
      this.showSpinner = true;
      await new Promise(resolve => {
        setTimeout(resolve, 2000)
      })
      this.showSpinner = false;
      this.showThankYou = true;
  }
};
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
