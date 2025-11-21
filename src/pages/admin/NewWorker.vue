<template>
  <div class="p-4">
    <!-- 신규 기사 등록 -->
    <div class="flex flex-col items-end gap-3">
      <!-- 신규 기사 입력폼 -->
      <div class="w-full bg-gray-100">
        <!-- 아이디 -->
        <div class="flex px-5 py-3 items-center gap-3">
          <p>아이디</p>
          <span class="text-[#296af1] font-semibold">clean{{ workersID }}</span>
          <span class="text-[14px] text-red-500">
            <i class="fa-solid fa-circle-exclamation"></i>
            아이디와 비밀번호(아이디 + !)는 자동으로 생성되며 기사가 최초 로그인 후 비밀번호 변경할
            것을 권합니다.
          </span>
        </div>
        <!-- 이름 -->
        <div class="flex px-5 py-3 items-center gap-3">
          <label for="name">이름</label>
          <input
            v-model="newWorkerName"
            id="name"
            class="bg-white border rounded-md border-gray-400 py-0.5"
            type="text" />
        </div>
        <!-- 생년월일 -->
        <div class="flex px-5 py-3 items-center gap-3">
          <label for="name">생년월일</label>
          <input
            v-model="newWorkerBirth"
            id="name"
            class="bg-white border rounded-md border-gray-400 py-0.5"
            type="text" />
        </div>
        <!-- 연락처 -->
        <div class="flex px-5 py-3 items-center gap-3">
          <label for="phone">연락처</label>
          <input
            v-model="newWorkerPhone"
            id="phone"
            class="bg-white border rounded-md border-gray-400 py-0.5"
            type="number" />
        </div>
        <!-- 이메일 -->
        <div class="flex px-5 py-3 items-center gap-3">
          <label for="email">이메일</label>
          <input
            v-model="newWorkerEmail"
            id="email"
            class="bg-white border rounded-md border-gray-400 py-0.5"
            type="email" />
        </div>
        <!-- 주소 -->
        <div class="flex px-5 py-3 items-center gap-3">
          <label for="address">주소</label>
          <input
            v-model="newWorkerAddress"
            id="address"
            class="bg-white border rounded-md w-[50%] border-gray-400 py-0.5"
            type="address" />
        </div>
        <!-- 첨부파일 -->
        <div class="flex px-5 py-3 items-center gap-3">
          <label>첨부파일</label>
          <input
            type="file"
            class="p-1.5 text-[rgba(0,0,0,0.25)] border-2 border-dashed border-[rgba(0,0,0,0.25)] rounded-lg cursor-pointer" />
        </div>
      </div>
      <div class="w-full bg-gray-100 flex px-5 py-3 gap-3">
        <label for="memo">메모</label>
        <textarea
          rows="5"
          v-model="newWorkerMemo"
          class="bg-white border rounded-md border-gray-400 py-0.5 w-[90%]"
          name="memo"
          id="memo"></textarea>
      </div>
      <!-- 목록 이동 버튼 -->
      <button
        @click="$router.push('workerlist')"
        class="bg-[#53698A] text-white px-2 py-1 rounded-md">
        목록
      </button>
    </div>
    <!-- 버튼 -->
    <div class="flex justify-center gap-3">
      <button @click="resetInput" class="bg-[#53698A] text-xl text-white px-10 rounded-md py-2">
        취소
      </button>
      <button @click="addWorker" class="bg-[#296af1] text-xl text-white px-10 rounded-md py-2">
        등록
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import workerData from "@/data/worker.json";

const workers = ref(workerData);
const workersID = ref(workers.value.length);

// input값 기본
const newWorkerName = ref("");
const newWorkerBirth = ref("");
const newWorkerPhone = ref("");
const newWorkerEmail = ref("");
const newWorkerAddress = ref("");
const newWorkerMemo = ref("");

// 취소 클릭시 입력값 초기화
const resetInput = () => {
  newWorkerName.value = "";
  newWorkerBirth.value = "";
  newWorkerPhone.value = "";
  newWorkerEmail.value = "";
  newWorkerAddress.value = "";
  newWorkerMemo.value = "";
};

// 등록 버튼 클릭시
const addWorker = () => {
  // 유효성 검사
  if (
    newWorkerName.value === "" ||
    newWorkerBirth.value === "" ||
    newWorkerPhone.value === "" ||
    newWorkerEmail.value === "" ||
    newWorkerAddress.value === ""
  ) {
    alert("정보를 모두 입력해주세요.");
    return;
  }
  workersID.value++;
  alert("기사 등록이 완료되었습니다.");
  resetInput();
};
</script>

<style scoped lang="scss">
.flex {
  p,
  label {
    font-size: 18px;
    color: #555555;
    width: 100px;
  }
}
.bg-gray-100 {
  div {
    border-bottom: 1px solid #d9d9d9;
    &:last-child {
      border: none;
    }
  }
}
</style>
