<template>
  <div v-if="open" class="modal mx-auto">
    <div class="backdrop" @click="$emit('close')" />
    <div class="shell overflow-hidden anim-scale-in position-relative rounded-0 rounded-md-2">
      <slot />
      <a @click="$emit('close')" class="position-absolute right-0 top-1 p-4 text-gray">
        <Icon name="close" />
      </a>
    </div>
  </div>
</template>

<script>
import { mapActions } from 'vuex';

export default {
  props: ['open'],
  watch: {
    open(val, prev) {
      if (val !== prev) this.toggleModal();
    },
  },
  methods: {
    ...mapActions(['toggleModal']),
  },
};
</script>

<style lang="scss">
.modal {
  position: fixed;
  display: flex;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  align-items: center;
  justify-content: center;
  z-index: 40;

  .backdrop {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: 99;
    background: rgba(0, 0, 0, 0.4);
  }

  .shell {
    border: 1px solid var(--border-color);
    background-color: var(--bg-color);
    padding-left: 0 !important;
    padding-right: 0 !important;
    max-width: 440px;
    overflow-y: auto !important;
    max-height: calc(100vh - 120px);
    display: flex;
    flex-direction: column;
    z-index: 999;
    margin: 0 auto;
    width: 100%;

    @media (max-width: 767px) {
      border: 0;
      width: 100% !important;
      max-width: 100% !important;
      max-height: 100% !important;
      min-height: 100% !important;
      margin-bottom: 0 !important;
    }

    .modal-body {
      flex: auto;
      text-align: initial;
      overflow-y: auto;
      overflow-x: hidden;
    }
  }
}
</style>
