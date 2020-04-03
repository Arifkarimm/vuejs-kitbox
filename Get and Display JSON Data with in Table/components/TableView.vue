<template>
  <div class="container mt-4" id="app">
    <table class="table table-bordered">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Name</th>
          <th scope="col">Email</th>
          <th scope="col">Website</th>
          <th scope="col">City</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user, index in users">
          <th scope="row">{{ index + 1 }}</th>
          <td>{{ user.name }}</td>
          <td>{{ user.email.toLowerCase() }}</td>
          <td>{{ user.website }}</td>
          <td>{{ user.address.city }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "Tableview",
  data() {
    return {
      users: []
    };
  },
  mounted: function() {
    axios
      .get("https://jsonplaceholder.typicode.com/users")
      .then(response => {
        this.users = response.data;
        console.log(response);
      })
      .catch(error => {
        console.log(error);
      });
  }
};
</script>

<style lang="scss" scoped>
</style>