<template>
  <div class="container m-2">
    <h1><i class="fa-solid fa-pen-to-square"></i>연락처 수정</h1>

    <!-- name -->
    <div class="mb-3 mt-3">
      <label for="name">name:</label>
      <input
        id="name"
        type="text"
        class="form-control"
        placeholder="이름을 입력하세요."
        v-model="name"
      />
    </div>

    <!-- tel -->
    <div class="mb-3 mt-3">
      <label for="tel">tel:</label>
      <input
        id="tel"
        type="number"
        class="form-control"
        placeholder="전화번호를 입력하세요."
        v-model="tel"
      />
    </div>

    <!-- address -->
    <div class="mb-3 mt-3">
      <label for="address">address:</label>
      <input
        id="address"
        type="text"
        class="form-control"
        placeholder="주소를 입력하세요."
        v-model="address"
      />
    </div>

    <!-- photo url -->
    <div class="mb-3 mt-3">
      <label for="photoUrl">photo url:</label>
      <input
        id="photoUrl"
        type="text"
        class="form-control"
        placeholder="사진의 url을 입력하세요."
        v-model="photo"
      />
    </div>

    <!-- 확인, 취소 버튼 -->
    <div class="text-center">
      <!-- 버튼 클릭 -> 입력받은 정보 매개변수로 전송 -->
      <button
        type="submit"
        class="btn btn-primary m-1"
        @click="editContact({ name, tel, address, photo })"
      >
        <i class="fa-solid fa-check"></i>
        확인
      </button>

      <router-link :to="'/contacts/detail'" class="btn btn-primary">
        <i class="fa-solid fa-rotate-left"></i>
        취소
      </router-link>
    </div>
  </div>
</template>

<script setup>
import axios from 'axios';
import { reactive } from 'vue';
import { useRoute, useRouter } from 'vue-router';

const BASEURL = '/api/contacts';
//현재 라우트 정보 가져오기
const currentRoute = useRoute();
//수정 -> 목록으로 이동하기 위해 선언
const router = useRouter();

//id 가져오기
const id = currentRoute.params.id;

//확인 버튼 클릭 시
const editContact = async ({ name, tel, address, photo }) => {
  //name, tel은 필수 입력 요소
  if (!name || name.trim() === '') {
    alert('이름은 반드시 입력해야 합니다.');
    return;
  } else if (!tel || tel.toString().trim() === '') {
    //tel(number) 값을 String으로 변경하여 판단
    alert('전화번호는 반드시 입력해야 합니다.');
    return;
  } else if (confirm('수정하시겠습니까?')) {
    //'확인' 누르면
    const payload = { name, tel, address, photo };
    console.log(payload);
    //데이터 수정
    await axios.put(BASEURL + `/${id}`, payload);

    //목록으로 이동
    router.push('/contacts');
  }
};
</script>
