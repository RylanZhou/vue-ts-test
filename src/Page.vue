<!-- Page.vue -->
<template>
  <div>
    <div>
      <span v-if="!content1IsEditing">{{ data.content1 }}</span>
      <input v-else type="text" v-model="content1Input" />

      <button v-if="!content1IsEditing" @click="toggleContent1Edit">
        Edit
      </button>
      <button v-else @click="saveContent1">
        Save
      </button>
    </div>

    <div>
      <span v-if="!content2IsEditing">{{ data.content2 }}</span>
      <input v-else type="text" v-model="content2Input" />

      <button v-if="!content2IsEditing" @click="toggleContent2Edit">
        Edit
      </button>
      <button v-else @click="saveContent2">
        Save
      </button>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'

@Component({ name: 'Navbar' })
export default class Page extends Vue {
  @Prop() data!: PageDataType

  content1IsEditing = false
  content1Input = ''
  content2IsEditing = false
  content2Input = ''

  toggleContent1Edit() {
    this.content1IsEditing = true
    this.content1Input = this.data.content1 || ''
  }

  toggleContent2Edit() {
    this.content2IsEditing = true
    this.content2Input = this.data.content2 || ''
  }

  saveContent1() {
    this.$emit('save-1', this.content1Input)
    this.content1IsEditing = false
    this.content1Input = ''
  }

  saveContent2() {
    this.$emit('save-2', this.content2Input)
    this.content2IsEditing = false
    this.content2Input = ''
  }
}
</script>

<style lang="scss"></style>
