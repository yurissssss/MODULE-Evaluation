<template>
  <div class="container m-2">
    <h1><i class="fa-solid fa-pen-to-square"></i> 새 연락처</h1>

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
        @click="addContact({ name, tel, address, photo })"
      >
        <i class="fa-solid fa-check"></i>
        확인
      </button>

      <router-link :to="'/contacts'" class="btn btn-primary">
        <i class="fa-solid fa-rotate-left"></i>
        취소
      </router-link>
    </div>
  </div>
</template>

<script setup>
import axios from 'axios';
import { reactive } from 'vue';
import { useRouter } from 'vue-router';

const BASEURL = '/api/contacts';
//추가 -> 목록으로 이동하기 위해 선언
const router = useRouter();

const states = reactive({ contacts: [] });

//확인 버튼 클릭 시
const addContact = async ({ name, tel, address, photo }) => {
  //name, tel은 필수 입력 요소
  if (!name || name.trim() === '') {
    alert('이름은 반드시 입력해야 합니다.');
    return;
  } else if (!tel || tel.toString().trim() === '') {
    //tel(number) 값을 String으로 변경하여 판단
    alert('전화번호는 반드시 입력해야 합니다.');
    return;
  } else if (confirm('저장하시겠습니까?')) {
    const payload = { name, tel, address, photo };
    console.log(payload);
    await axios.post(BASEURL, payload);

    //기존의 데이터 가져오기
    const response = await axios.get(BASEURL);
    states.contacts = response.data;

    //contacts에 데이터 추가
    states.contacts.push({ name, tel, address, photo });
    //목록으로 이동
    router.push('/contacts');
  }
};
</script>
