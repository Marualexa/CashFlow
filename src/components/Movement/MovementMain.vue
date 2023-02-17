<template>
  <div class="movements">
    <h2 class="title">Historial</h2>
    <div class="content">
      <Operacion
        v-for="{ id, title, description, amount } in movements"
        :key="id"
        :id='id'
        :title="title"
        :description='description'
        :amount='amount'
        @remove="remove"
        >
      </Operacion>
    </div>
  </div>
</template>

<script setup>
import { toRefs, defineProps, defineEmits } from "vue";
import Operacion from './OperacionMoven.vue';


const props = defineProps({
  movements: {
    type: Array,
    default: () => [],
  },
});

const { movements } = toRefs(props);

const emit = defineEmits(["remove"])

const remove = (id) => {
  emit("remove", id);
}
</script>

<style scoped>
.movements {
  max-height: 100%;
  padding: 0 8px;
  margin-bottom: 14px;
  color: var(--backgrount-1);
}
.title {
  margin: 8px 16px 24px 16px;
  color: #fff;
}
.content {
  max-height: 68vh;
  display: flex;
  flex-direction: column;
  gap: 8px;
  overflow-y: scroll;
}
</style>
