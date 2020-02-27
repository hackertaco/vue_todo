<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" @keyup.enter="addTodo" />

    <span class="addContainer">
      <i v-on:click="addTodo" class="addBtn fas fa-plus"></i>
    </span>

    <Modal v-if="showModal" @close="showModal = false">
      <h3 slot="header">
        경고!
        <i class="fas fa-times closeModalBtn" @click="showModal=false"></i>
      </h3>
      <h4 slot="body">아무 내용이 없네요!</h4>
      <div slot="footer">copyright@hackertaco</div>
    </Modal>
  </div>
</template>

<script>
import Modal from "./common/Modal.vue";
export default {
  data() {
    return {
      newTodoItem: "",
      showModal: false
    };
  },
  components: {
    Modal
  },
  methods: {
    addTodo() {
      if (this.newTodoItem !== "") {
        this.$emit("addTodoItem", this.newTodoItem);
        this.clearInput();
      } else {
        this.showModal = !this.showModal;
      }
    },
    clearInput() {
      this.newTodoItem = ""; //분할해준다 기능을
    }
  }
};
</script>

<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  background: #fff;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  border-style: none;
  font-size: 0.9rem;
}
.addContainer {
  float: right;
  background: linear-gradient(to right, #6478fb, #8763fb);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}
.addBtn {
  color: #fff;
  vertical-align: middle;
}
.closeModalBtn {
  color: #42b983;
}
</style>