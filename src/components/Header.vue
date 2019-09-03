<template>
  <div>
    <h1>ToDoリスト</h1>
    <label v-for="label in options" class="bbb" v-bind:key="label.value">
      <input
        type="radio"
        v-model="current"
        v-bind:value="label.value"
        v-on:click="scurrent(label.value)"
      />
      {{ label.label }}
    </label>
    （{{ counter }} 件を表示）
  </div>
</template>

<script lang="ts" type="module">
import { Component, Prop, Vue, Emit } from "vue-property-decorator";
import option from "../Options";

@Component
export default class Header extends Vue {
  @Prop() counter!: number;
  current: number = -1;
  options = option;

  @Emit()
  scurrent(current: number): number {
    return current;
  }
}
</script>
