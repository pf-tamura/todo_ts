<template>
  <table>
    <thead>
      <tr>
        <th v-for="menu in ths" v-bind:key="menu.id">
          <button v-on:click="s_id(menu)" type="button" class="aaa">{{ menu.value }}</button>
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in computedTodos" v-bind:key="item.id" v-bind:class="{done:item.state}">
        <th>{{ item.id }}</th>
        <td>{{ item.comment }}</td>
        <td class="state">
          <button v-on:click="s_state(item)">{{ labels[item.state] }}</button>
        </td>
        <td>{{ item.date }}</td>
        <td>{{ getDate(item.datef) }}</td>
        <td></td>
        <td class="button">
          <button v-on:click="s_remove(item)">削除</button>
        </td>
      </tr>
    </tbody>
  </table>
</template>
<script lang="ts">
import { Component, Prop, Vue, Emit } from "vue-property-decorator";
// import Header from "./components/Header.vue";
import option from "../Options";

@Component({
  components: {
    // Header
  }
})
export default class Main extends Vue {
  @Prop() computedTodos!: any[];
  ths: any = [
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

  getDate(datef: number): string {
    if (datef === -1) {
      return "未完了";
    } else {
      let f = new Date(datef);
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
  s_state(state: any): any {
    return state;
  }

  @Emit()
  s_id(menu: any): any {
    return menu.id;
  }
  @Emit()
  s_remove(item: any): any {
    return item;
  }
}
</script>
