<template>
  <form class="card card-w30" @submit.prevent="addContent">
    <div class="form-control">
      <label for="type">Тип блока</label>
      <select id="type" v-model="type">
        <option value="title">Заголовок</option>
        <option value="subtitle">Подзаголовок</option>
        <option value="avatar">Аватар</option>
        <option value="text">Текст</option>
      </select>
    </div>

    <div class="form-control">
      <label for="value">Значение</label>
      <textarea id="value" rows="3" v-model="text"></textarea>
    </div>

    <button class="btn primary" :disabled="!isValidValue">Добавить</button>
  </form>
</template>

<script>
export default {
  emits: ['add-title-or-avatar', 'add-description'],
  data () {
    return {
      type: 'title',
      text: ''
    }
  },
  methods: {
    addContent () {
      let method = ''
      if (this.type === 'title' || this.type === 'avatar') {
        method = 'add-title-or-avatar'
      } else {
        method = 'add-description'
      }
      this.$emit(method, this.type, this.text)
      this.type = 'title'
      this.text = ''
    }
  },
  computed: {
    isValidValue () {
      return this.text.length > 3
    }
  }
}
</script>
