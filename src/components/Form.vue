<template>
  <div>
    <h2>新しい作業の追加</h2>
    <form class="add-form" v-on:submit.prevent="doAdd">
      コメント
      <input type="text" ref="comment" />
      <button type="submit">追加</button>
    </form>
  </div>
</template>

<script lang="ts" type="module">
import { Component, Prop, Vue, Emit } from "vue-property-decorator";
let total: number = 0;

@Component
export default class Form extends Vue {
  @Prop() comment!: string;
  todos: any[] = [];
  itemId = 0;
  doAdd(): void {
    var comment: HTMLInputElement = this.$refs.comment as HTMLInputElement;
    if (!comment.value) {
      return;
    }
    var d = new Date();
    this.todos.push({
      id: this.itemId++,
      comment: comment.value,
      state: 0,
      dateAdded:
        d.getFullYear() +
        "/" +
        d.getMonth() +
        "/" +
        d.getDate() +
        "/" +
        d.getHours() +
        ":" +
        d.getMinutes(),
      // dateAdded: d.getTime(),
      dateEnd: -1
    });
    comment.value = "";
    this.notify();
  }

  @Emit()
  notify(): any[] {
    return this.todos;
  }
}
</script>
