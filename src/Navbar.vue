<!-- Navbar.vue -->
<template>
  <div>
    <ul>
      <li
        v-for="tab in pageData"
        :key="tab.id"
        class="tab"
        @click="() => handleTabClick(tab.id)"
      >
        {{ tab.tabName }}
      </li>
      <li>
        <input type="text" v-model="inputTab" /><button @click="handleAddClick">
          Add
        </button>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator'

@Component({ name: 'Navbar' })
export default class Navbar extends Vue {
  @Prop({ default: () => [] }) pageData?: PageDataType

  inputTab = ''

  handleAddClick() {
    this.$emit('add', this.inputTab)
    this.inputTab = ''
  }

  handleTabClick(id: string) {
    this.$emit('change', id)
  }
}
</script>

<style lang="scss" scoped>
ul {
  display: flex;
  list-style: none;

  li {
    &.tab {
      width: 100px;
      margin: 0 10px;
      background-color: coral;

      &:hover {
        cursor: pointer;
      }
    }
  }
}
</style>
