<template>
  <button @click="showModal = true">Agregar movimiento</button>
  <teleport to="#app">
    <Modal v-show="showModal" @close="showModal = false">
        <form @submit.prevent="submit">
            <div class="field">
                <label for="">Titulo</label>
                <input type="text" v-model='title' />
            </div>
            <div class="field">
                <label for="">Monto</label>
                <input type="number" v-model='amount' />
            </div>
            <div class="field">
                <label for="">Descripción</label>
                <textarea rows="4" v-model="description"></textarea>
            </div>
            <div class="field">
                <label class="radio-label">
                    <input type="radio" v-model="movementType" value="Ingreso">
                    <span>Ingreso</span>
                </label>
            </div>
            <div class="field">
                <label class="radio-label">
                    <input type="radio" v-model="movementType" value="Gasto">
                    <span>Gasto</span>
                </label>
            </div>
            <div class="action">
                <button>Agregar movimiento</button>
            </div>
        </form>
    </Modal>
  </teleport>
</template>

<script setup>
import { ref, defineEmits } from "vue";
import Modal from "./ModalMovie.vue";

const showModal = ref(false);
const title = ref('');
const amount = ref(0);
const description = ref('');
const movementType = ref('Ingreso');

const emit = defineEmits(["create"]);

const submit = () => {
    showModal.value = !showModal.value;
    emit("create", {
    title: title.value,
    description: description.value,
    amount: movementType.value === "Ingreso" ? amount.value : -amount.value,
    time: new Date(),
    id: new Date(),
  });
  title.value = "";
  description.value = "";
  amount.value = "";
  movementType.value = "Ingreso";
}
</script>

<style scoped>
button {
  color: white;
  font-size: 1.0rem;
  background-color: var(--backgrount-2);
  border: none;
  width: 100%;
  padding: 24px 60px;
  border-radius: 60px;
  box-sizing: border-box;
}
button:hover {
  background-color: white;
  color: var(--backgrount-2);
}
form {
  font-size: 1.02rem;
  color: var(--backgrount-1);
  width: 100%;
}
form .action {
  padding: 0 24px;
}
.field {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  padding: 16px 24px;
}
label {
  margin-bottom: 8px;
}
input,
textarea {
  font-size: 1.24rem;
  border: 2px solid var(--backgrount-2);
  color: var(--backgrount-1);
  border-radius: 8px;
  padding: 8px;
}
input[type="number"] {
  text-align: right;
  color: var(--backgrount-1);
}
.radio-label {
  display: flex;
  align-items: center;
  margin-top: 8px;
}
.radio-label span {
  margin-top: 4px;
  margin-left: 8px;
}
input[type="radio"] {
  appearance: none;
  width: 1.24rem;
  height: 1.24rem;
  color: var(--backgrount-2);
  border: 2px solid var(--backgrount-2);
  border-radius: 50%;
}
input[type="radio"]:checked {
  background-color: var(--backgrount-2);
}
</style>
