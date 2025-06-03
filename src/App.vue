<template>
  <h1>lu-6</h1>

  <TModal :show="showModal" title="modal 1" msg="lorem ipsum" @close-me="closeModal" />

  <TModal :show="showModal2" title="modal 2" @close-me="showModal2 = false">
    <label>first name</label>
    <input type="text">
  </TModal>

  <TModal
    :show="fruitModalShow"
    title="potvrď, prosím"
    :msg="fruitModalMsg"
    okBtnLabel="Ano"
    cancelBtnLabel="Ne"
    @close-me="fruitModalShow = false"
    @cancel-btn-clicked="fruitModalShow = false"
    @ok-btn-clicked="deleteFruit"
  />

  <button @click="openModal">open modal 1</button>
  <button @click="showModal2 = true">open modal 2</button>

  <ul>
    <li
      v-for="(fruit, i) in fruits"
      :key="i + fruit"
      @click="onFruitClick(fruit)"
    >{{ fruit }}</li>
  </ul>

  <!-- po kliknutí na li otevřít modal a ověřit, jestli chce uživatel smazat dané ovoce
    možnost Ano, ne
    Ano - smažeme ovoce z pole fruits
    Ne - zavřeme modál a nic dál
    -->

  <!-- <TComponent header="i am header">
    <template v-slot:content>
      <button>click me</button>
      <button>click me</button>
      <input>
    </template>
    <template v-slot:footer>
      <p>Lorem ipsum dolor sit, amet consectetur adipisicing elit. Fuga repellendus vitae deleniti reiciendis, autem hic expedita iste ipsa quisquam ea mollitia reprehenderit cumque officia cum facilis et aperiam optio dolore?</p>
    </template>

  </TComponent> -->
</template>

<script>

import TModal from '@/components/TModal.vue'
import TComponent from '@/components/TComponent.vue'

export default {
  name: 'App',
  data() {
    return {
      showModal: false,
      showModal2: false,
      fruits: ['švestka', 'jablko', 'hruška', 'pomeranč'],
      fruitModalShow: false,
      fruitModalMsg: '',
      fruitToDelete: null
    }
  },
  methods: {
    openModal() {
      this.showModal = true
    },
    closeModal() {
      this.showModal = false
    },
    onFruitClick(fruit) {
      this.fruitToDelete = fruit
      this.fruitModalMsg = 'chceš opravdu smazat položku ' + fruit + '?'
      this.fruitModalShow = true
    },
    deleteFruit() {
      const index = this.fruits.indexOf(this.fruitToDelete)
      this.fruits.splice(index, 1)
      this.fruitModalShow = false
      this.fruitToDelete = ''
    }
  },
  components: { TModal, TComponent }
}

</script>