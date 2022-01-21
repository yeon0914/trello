<template>
  <Modal>
    <div slot="header">
      <h2>
        Create new board
        <a href="" class="modal-default-button" 
          @click.prevent="SET_IS_ADD_BOARD(false)">&times;</a>
      </h2>
    </div>
    <div slot="body">
      <form id="add-board-form" 
        @submit.prevent="addBoard">
        <input class="form-control" type="text" v-model="input" ref="input">
      </form>
    </div>
    <div slot="footer">
      <button class="btn-modal" :class="{'btn-success': valid}" type="submit" 
        form="add-board-form" :disabled="!valid">
        Create Board</button>
    </div>
  </Modal>
</template>

<script>
import { mapMutations, mapActions } from "vuex";
import Modal from "./Modal.vue";

export default {
  components: {
    Modal
  },
  data() {
    return {
      input: "",
      valid: false
    };
  },
  watch: {
    input(v) {
      this.valid = v.trim().length > 0;
    }
  },
  mounted() {
    this.$refs.input.focus();
  },
  methods: {
    ...mapMutations(["SET_IS_ADD_BOARD"]),
    ...mapActions(["ADD_BOARD", "FETCH_BOARDS"]),
    addBoard() {
      this.ADD_BOARD({ title: this.input })
        .then(({ id }) => this.$router.push(`/b/${id}`))
        .catch(err => console.error(err))
        .finally(() => this.SET_IS_ADD_BOARD(false));
    }
  }
};
</script>

<style>
.btn-modal {
  border-radius: 3px;
  padding: 6px 8px;
  border: none;
  display: inline-block;
  font-size: 14px;
  line-height: 20px;
  font-weight: 700;
  cursor: pointer;
  background-color: #ff9f74;
  color: white;
}
</style>
