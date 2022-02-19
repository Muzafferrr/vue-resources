<template>
  <div id="app">
    <ul v-for="item in items" :key="item.id">
      <li>
        {{item.email}} <br>
        <img :src="item.avatar" class="image">
      </li>
    </ul>
    <input type="text" v-model="name"><br>
    <input type="text" v-model="job"><br>
    <button @click="sendUser">Send User</button>
    <hr>
    <input type="text" v-model="id"><br>
    <button @click="deleteUser">Delete</button>
    <hr>
    <input type="text" v-model="name"><br>
    <input type="text" v-model="job"><br>
    <input type="text" v-model="id"><br>
    <button @click="updateUser">Update User</button>
  </div>
</template>

<script>
export default {
  name: "App",
  data(){
    return{
      items: [],
      name:'',
      job:'',
      id:''
    }
  },
  beforeCreate() {
    {
      this.$http.get("https://reqres.in/api/users").then(
        (response) => {
          this.items.push(...response.body.data)
        },
        (response) => {
          console.log(response.body.data);
        }
      );
    }
  },
  methods:{
    sendUser(){
      this.$http.post("https://reqres.in/api/users", {name:this.name, job:this.job})
      .then(response => {
        console.log(response.body);
      }, () => {
        console.log('error');
      })
    },
    deleteUser(){
      this.$http.delete('https://reqres.in/api/users/' + this.id)
      .then(response => {
        console.log(response);
      })
    },
    updateUser(){
      this.$http.put("https://reqres.in/api/users/" + this.id, {name:this.name, job:this.job})
      .then(response => {
        console.log(response);
      }, () => {
        console.log('error');
      })
    }
  }
};
</script>
<style scoped>
.image{
  width: 100px;
  height: auto;
}
</style>