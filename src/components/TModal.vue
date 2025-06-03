<template>
  <transition name="fade" @after-enter="bodyShow = true">
    <div v-if="show" @click="onBgClick" class="modal-bg">

      <transition name="slide-down" @after-leave="emitClose">
        <div v-if="bodyShow" class="modal-body" ref="modalBody">
          <div class="modal-header">
            <div>{{ title }}</div>
            <div @click="onClosingXClicked" class="closing-x">X</div>
          </div>
          <div v-if="msg" class="modal-center">
            {{ msg }}
          </div>
          <div v-else class="modal-center">
            <slot></slot>
          </div>
          <div class="modal-footer">
            <button v-if="okBtnShow" @click="onOkClick">{{ okBtnLabel }}</button>
            <button v-if="cancelBtnShow" @click="onCancelClick">{{ cancelBtnLabel }}</button>
          </div>
        </div>
      </transition>
    </div>
  </transition>
</template>

<script>

export default {
  name: 'TModal',
  props: {
    show: {
      type: Boolean,
      default: false
    },
    okBtnShow: {
      type: Boolean,
      default: true
    },
    cancelBtnShow: {
      type: Boolean,
      default: true
    },
    okBtnLabel: {
      type: String,
      default: 'OK'
    },
    cancelBtnLabel: {
      type: String,
      default: 'cancel'
    },
    title: {
      type: String
    },
    msg: {
      type: String,
      default: ''
    }
  },
  data() {
    return {
      bodyShow: false
    }
  },
  methods: {
    onClosingXClicked() {
      this.bodyShow = false
    },
    onOkClick() {
      this.$emit('ok-btn-clicked')
    },
    onCancelClick() {
      this.$emit('cancel-btn-clicked')
    },
    onBgClick(e) {
      // ??? je event.target uvnitř modal-body???
      // el.contains(el2)
      const modalBody = this.$refs.modalBody
      if (modalBody && !modalBody.contains(e.target)) {
        this.bodyShow = false
      }
    },
    emitClose() {
      this.$emit('close-me')
    }

  }
}

</script>

<style scoped lang="stylus">
@import '../styles/transitions.styl'

.modal-bg {
  /* opacity: .3; */
  background: rgba(0, 0, 0, .3);
  width: 100vw;
  height: 100vh;
  position: fixed;
  top: 0;
  left: 0;
}

.modal-body {
  background: white;
  width: 70%;
  max-width: 600px;
  min-width: 300px;
  min-height: 300px;
  margin: 3rem auto;
  border-radius: 10px;
  box-shadow: rgba(50, 50, 93, 0.25) 0px 13px 27px -5px, rgba(0, 0, 0, 0.3) 0px 8px 16px -8px;
  display: flex;
  flex-direction: column;
}

.modal-header, .modal-center {
  border-bottom: 2px solid #898989;
}

.modal-header, .modal-footer {
  flex-basis: 80px;
  flex-grow: 0;
  display: flex;
  align-items: center;
}

.modal-center {
  flex-grow: 1;
}

.modal-header,
.modal-footer,
.modal-center {
  padding: 1rem;
}

.modal-header {
  font-size: 1.5rem;
  justify-content: space-between;
}

.modal-header div {
  font-weight: bold;
}

.modal-footer {
  justify-content: flex-end;
  gap: 1rem;
}

.closing-x {
  cursor: pointer;
  padding: .3rem .5rem;
}






</style>
