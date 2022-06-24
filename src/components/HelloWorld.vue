<template>
  <div class="hello">
    <button @click="login()">login</button>
    <p><strong>Token:</strong> {{ token }}</p>
    <button @click="getData()">getdata</button>
    <table>
      <tr>
        <th>Donor Name</th>
        <th>Donor's Age</th>
        <th>Donor's Sex</th>
        <th>Donor Phone</th>
        <th>Donor Relative</th>
      </tr>
      <tr v-for="data in tableData" :key="data">
        <td>{{ data.donor_name }}</td>
        <td>{{ data.age }}</td>
        <td>{{ data.sex }}</td>
        <td>{{ data.phone_no }}</td>
        <td>{{ data.donor_relation_with_the_guardian }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "HelloWorld",
  data() {
    return {
      token: "",
      tableData: [],
    };
  },

  methods: {
    login() {
      axios
        .post("http://143.110.249.241:3002/login", {
          email: "bikanernew@gmail.com",
          password: "12345678",
        })
        .then((res) => {
          this.token = res.data.token;
          localStorage.setItem("token", res.data.token);
        });
    },

    getData() {
      axios
        .get("http://143.110.249.241:3002/donorNotification/fetch")
        .then((res) => {
          console.table(res.data.data);
          this.tableData = res.data.data;
        });
    },
  },
};
</script>
<style scoped>
td {
  padding: 5px 5px;
  margin: 5px;
  border: 1px solid black;
}
</style>
