<template>
  <div class="container m-2">
    <h1><i class="fa-solid fa-address-book"></i> 연락처</h1>

    <div style="display: flex">
      <!-- 사진 -->
      <img
        :src="contact.photo"
        style="width: 150px; height: 150px; border-radius: 10px"
        alt="idphoto"
      />

      <div class="ms-5 w-50">
        <!-- 정보 -->
        <table class="table table-borderless">
          <tr>
            <td>ID</td>
            <td>{{ contact.id }}</td>
          </tr>
          <tr>
            <td>name</td>
            <td>{{ contact.name }}</td>
          </tr>
          <tr>
            <td>tel</td>
            <td>{{ contact.tel }}</td>
          </tr>
          <tr>
            <td>address</td>
            <td>{{ contact.address }}</td>
          </tr>
        </table>

        <!-- 목록, 수정, 삭제 버튼 -->
        <div>
          <router-link :to="'/contacts'" class="btn btn-primary m-1">
            <i class="fa-solid fa-list"></i>
            목록
          </router-link>
          <router-link
            :to="'/contacts/edit/' + contact.id"
            class="btn btn-primary m-1"
          >
            <i class="fa-solid fa-pen-to-square"></i>
            수정
          </router-link>
          <button class="btn btn-danger m-1" @click="deleteContact(contact.id)">
            <i class="fa-solid fa-trash-can"></i>
            삭제
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import axios from 'axios';
import { ref } from 'vue';
import { useRoute, useRouter } from 'vue-router';

const BASEURL = '/api/contacts';
//현재 라우트 정보 가져오기
const currentRoute = useRoute();
//삭제버튼 -> 목록으로 이동하기 위해 선언
const router = useRouter();

const contact = ref({});

//클릭한 데이터의 id 가져오기
const id = currentRoute.params.id;
//console.log(id);

//정보 가져오기
const fetchContact = async () => {
  //선택한 name의 데이터 가져오기
  const response = await axios.get(BASEURL + `/${id}`);
  contact.value = response.data;
  //console.log(contact.name);
};

fetchContact();

//삭제 버튼 이벤트
const deleteContact = async (id) => {
  //만약 알림창에서 '확인'을 누르면
  if (confirm('정말 삭제하시겠습니까?')) {
    //삭제
    await axios.delete(BASEURL + `/${id}`);
    //목록으로 이동
    router.push('/contacts');
  }
};
</script>
