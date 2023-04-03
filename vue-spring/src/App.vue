<template>
  <table class="table">
    <thead>
      <tr>
        <th scope="col">id</th>
        <th scope="col">name</th>
        <th scope="col">job</th>
        <th scope="col">home</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="member in members" :key="member.id">
        <th scope="row">{{member.id}}</th>
        <td>{{member.name}}</td>
        <td>{{member.job}}</td>
        <td>{{member.home}}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
import axios from "axios";
import {ref} from 'vue';

export default {
  setup(){
    axios.defaults.baseURL = 'http://localhost:8000';
    axios.defaults.headers.post['Content-Type'] ='application/json;charset=utf-8';
    axios.defaults.headers.post['Access-Control-Allow-Origin'] = '*';

    const members = ref([]);

    const getMembers = async () => {
      try{
        const res = await axios.get('/members');
        members.value = {...res.data};
      }catch(err){
        console.log(err);
      }
      
    }

    getMembers();

    return {
      members
    }
  }
}
</script>

<style>

</style>
