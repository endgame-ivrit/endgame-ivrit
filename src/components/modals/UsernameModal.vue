<script>
import ModalWrapperChoice from "@/components/modals/ModalWrapperChoice";

export default {
  name: "UsernameModal",
  components: {
    ModalWrapperChoice
  },
  data() {
    return {
      hasSeenModal: false,
      input: "",
      username: ""
    };
  },
  computed: {
    notEmpty() {
      return this.input !== "";
    },
  },
  methods: {
    saveUsername() {
      if (this.notEmpty) this.username = this.input;
      if (this.notEmpty) player.username = this.username;
      if (this.notEmpty) this.hasSeenModal = true;
      this.input = "";
      player.options.hasSeenUsernameModal = this.hasSeenModal;
      if (player.options.hasSeenUsernameModal) player.introFrozen = false;
    },
  },
};
</script>

<template>
  <ModalWrapperChoice
    :show-cancel="!notEmpty"
    :show-confirm="notEmpty"
    confirm-class="o-primary-btn--width-medium c-modal__confirm-btn c-modal-username-btn"
    @confirm="saveUsername"
  >
    <template #header>
      הזן שם משתמש
    </template>
    <div class="c-modal-message__text" dir="rtl">
      אנא אשר את שם המשתמש שלך.
      <span class="c-modal-username-danger">ניתן לבחור את שם המשתמש שלך רק פעם אחת.</span>
      הקלד את שם המשתמש הרצוי לאישור.
      <div class="c-modal-username-danger">
        פעולה זו בלתי הפיכה
      </div>
    </div>
    <input
      ref="input"
      v-model="input"
      type="text"
      class="c-modal-input c-modal-username__input"
      @keyup.esc="emitClose"
    >
    <div class="c-modal-username-info">
      <div
        v-if="notEmpty"
        class="c-modal-username-danger"
      >
        שם המשתמש אושר - האם אתה בטוח שזה שם המשתמש הרצוי לך?
      </div>
      <div v-else>
        אנא הקלד משהו.
      </div>
    </div>
    <template #confirm-text>
      אשר
    </template>
  </ModalWrapperChoice>
</template>
