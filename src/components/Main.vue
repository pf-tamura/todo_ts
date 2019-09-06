<template>
  <table>
    <thead>
      <tr>
        <th v-for="column in columns" v-bind:key="column.id">
          <button v-on:click="id(column)" type="button" class="aaa">
            {{ column.value }}
          </button>
        </th>
      </tr>
    </thead>
    <tbody>
      <tr
        v-for="item in computedTodos"
        v-bind:key="item.id"
        v-bind:class="{ done: item.state }"
      >
        <th>{{ item.id }}</th>
        <td>{{ item.comment }}</td>
        <td class="state">
          <button v-on:click="state(item)">{{ labels[item.state] }}</button>
        </td>
        <td>{{ item.dateAdded }}</td>
        <td>{{ getDate(item.dateEnd) }}</td>
        <td></td>
        <td class="button">
          <button v-on:click="remove(item)">削除</button>
        </td>
      </tr>
    </tbody>
  </table>
</template>
<script lang="ts">
import { Component, Prop, Vue, Emit } from "vue-property-decorator";
import option from "../Options";

@Component
export default class Main extends Vue {
  @Prop() computedTodos!: any[];

  columns: any = [
    { id: 0, value: "ID" },
    { id: 1, value: "コメント" },
    { id: 2, value: "状態" },
    { id: 3, value: "追加日" },
    { id: 4, value: "完了した日" },
    { id: 5, value: "-" }
  ];

  get labels(): any[] {
    return option.reduce(function(a, b) {
      return Object.assign(a, { [b.value]: b.label });
    }, {});
  }

  getDate(dateEnd: number): string {
    if (dateEnd === -1) {
      return "未完了";
    } else {
      let f = new Date(dateEnd);
      return (
        f.getFullYear() +
        "/" +
        f.getMonth() +
        "/" +
        f.getDate() +
        "/" +
        f.getHours() +
        ":" +
        f.getMinutes()
      );
    }
  }

  @Emit()
  state(state: any): any {
    return state;
  }

  @Emit()
  id(type: any): any {
    return type.id;
  }
  @Emit()
  remove(item: any): any {
    return item;
  }
}
</script>
