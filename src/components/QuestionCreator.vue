<script setup>
import { ref } from 'vue'
import TextQuestion from './form/TextQuestion.vue'
import SelectQuestion from './form/SelectQuestion.vue'

const emit = defineEmits(['add-question'])

const id = ref('')
const title = ref('')
const description = ref('')
const type = ref('')
const placeholder = ref('')
const options = ref([])

const typeOptions = [
  { value: 'radio', label: 'Выбор (radio)' },
  { value: 'checkbox', label: 'Выбор нескольких (checkbox)' },
  { value: 'select', label: 'Выбор (select)' },
  { value: 'text', label: 'Текстовый (text)' },
]

function addQuestion(id, title, description, type, value) {
  const key = type === 'text' ? 'placeholder' : 'options'
  emit('add-question', { id, title, description, type, [key]: value })
}
</script>

<template>
  <div class="bg-white rounded-2xl shadow p-6">
    <h2 class="text-xl font-semibold mb-4">Добавить вопрос</h2>
    <form class="space-y-3">
      <TextQuestion placeholder="ID вопроса" v-model="id" />
      <TextQuestion placeholder="Заголовок вопроса" v-model="title" />
      <TextQuestion placeholder="Описание вопроса" v-model="description" />
      <SelectQuestion :options="typeOptions" v-model="type" />
      <TextQuestion placeholder="Placeholder" v-model="placeholder" v-if="type === 'text'" />
      <TextQuestion placeholder="Options" v-model="options" v-else />
    </form>
    <button
      class="mt-6 px-4 py-2 rounded bg-gray-100 hover:bg-gray-200"
      @click="addQuestion(id, title, description, type, type === 'text' ? placeholder : options)"
    >
      Добавить вопрос
    </button>
  </div>
</template>
