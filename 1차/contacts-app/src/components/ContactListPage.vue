<template>
  <div class="container m-2">
    <h1><i class="fa-solid fa-address-book"></i> 연락처</h1>

    <table class="table mt-5">
      <thead>
        <tr>
          <th>id</th>
          <th>name</th>
          <th>tel</th>
        </tr>
      </thead>
      <tbody>
        <!-- 백엔드로부터 가져온 데이터 표에 출력 -->
        <tr v-for="contact in states.contacts" :key="contact.id">
          <!-- id -->
          <td>{{ contact.id }}</td>
          <!-- photo & name -->
          <td>
            <img
              :src="contact.photo"
              style="width: 24px; height: 24px"
              class="rounded-circle me-2"
              alt="idphoto"
            />
            <!-- name 클릭하면 '상세보기' 페이지로 이동 -->
            <router-link :to="'/contacts/detail/' + contact.id">
              {{ contact.name }}
            </router-link>
          </td>
          <td>{{ contact.tel }}</td>
        </tr>
      </tbody>
    </table>

    <!-- 새 연락처 추가 버튼 -->
    <!-- <div class="text-end"> -->
    <div style="text-align: right">
      <!-- 누르면 '연락처 추가'페이지로 이동 -->
      <router-link :to="'/contacts/write'" class="btn btn-primary">
        <i class="fa-solid fa-pen-to-square"></i>
        새 연락처
      </router-link>
    </div>
  </div>
</template>

<script setup>
import axios from 'axios';
import { onMounted, reactive } from 'vue';

const BASEURL = '/api/contacts';
const states = reactive({ contacts: [] });

//백엔드로부터 데이터 가져오기
const fetchContacts = async () => {
  const response = await axios.get(BASEURL);
  states.contacts = response.data;
  //   console.log(states.contacts);
};

fetchContacts();
</script>
