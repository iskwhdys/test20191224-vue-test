<template>
  <div id="field">

    <!-- <h3>検索条件</h3>
    <div>
      <label>Search</label>
      <input v-model="searchText" placeholder="text" type="text" />
      <button @click="onClickSearch">Search</button>
    </div> -->

    <router-view></router-view>
    <button @click="onClickUpdate">データを反映</button><br />
    <br />
    <table border="1">
      <thead>
        <tr>
          <td>productCode</td>
          <td>inventoryNumber</td>
          <td>quantity</td>
          <td>削除</td>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="item in items"
          :key="item.productCode + item.inventoryNumber"
        >
          <!-- 
            keyとなる項目を編集するとフォーカスが外れるのでreadonly https://teratail.com/questions/182565
            <td><input readonly v-model="item.productCode"/></td>
            td><input readonly v-model="item.inventoryNumber"/></td>
          -->
          <td>{{ item.productCode }}</td>
          <td>{{ item.inventoryNumber }}</td>
          <td>
            <input @change="onInputChange(item)" v-model="item.quantity" />
          </td>
          <td><button @click="onClickDelete(item)">✖</button></td>
        </tr>
      </tbody>
    </table>

    <br />
    <button @click="onClickAdd">レコード追加</button><br />
    <table border="1">
      <thead>
        <tr>
          <td>productCode</td>
          <td>inventoryNumber</td>
          <td>quantity</td>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td><input v-model="addItem.productCode" /></td>
          <td><input v-model="addItem.inventoryNumber" /></td>
          <td><input v-model="addItem.quantity" /></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import axios from "axios";

@Component
export default class Home extends Vue {
  // axios用の接続先
  dbHost: string = "http://localhost:8081/api/";
  dbInventory: string = this.dbHost + "inventory";

// 入力された検索ワード
  searchText: string = "";
  //
  items = [{ productCode: "", inventoryNumber: "", quantity: "" }];
  //
  addItem = { productCode: "", inventoryNumber: "", quantity: "" };

  async created() {
    console.log("created-start");

    this.items = (await axios.get(this.dbInventory, {})).data;

    console.log("created-end");
  }

  // 検索ボタンの押下
  async onClickSearch() {
    console.info("onClickSearch-start");

    console.info("onClickSearch-end");
  }

  async onClickDelete(item: any) {
    console.log("onClickDelete-start");

    // await axios.delete(this.dbInventory, item);

/*
    const index = this.items.findIndex(
      i =>
        i.productCode === item.productCode &&
        i.inventoryNumber === item.inventoryNumber
    );
    console.log(index);

    const removedUser = this.items.splice(index, 1);
    
    console.log(this.items);

    console.log(removedUser);
    */
    console.log("onClickDelete-end");
  }

  async onInputChange(item: any) {
    console.log("onInputChange-start");

    console.log(item);

    console.log("onInputChange-end");
  }

  async onClickUpdate() {
    console.log("onClickUpdate-start");
    console.log(this.items);

    await axios.post(this.dbInventory, this.items);

    console.log("onClickUpdate-end");
  }

  async onClickAdd() {
    console.log("onClickAdd-start");
    console.log(this.addItem);

    this.items.push(this.addItem);

    console.log("onClickAdd-end");
  }
}
</script>

<style lang="scss">
#field {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
}
</style>
