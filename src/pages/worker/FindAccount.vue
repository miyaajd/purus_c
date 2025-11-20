<template>
  <div class="w-full flex justify-center bg-white relative">
    <!-- 440 고정 모바일 레이아웃 -->
    <div class="w-full max-w-[440px] min-h-screen bg-white flex flex-col items-center pt-10">

      <!-- 탭 메뉴 -->
      <div class="w-full flex justify-center border-b border-gray-300">
        <div class="flex w-[260px] justify-between">
          <button
            class="pb-2 text-[17px] font-semibold border-b-2"
            :class="tab === 'id' ? 'text-blue-600 border-blue-600' : 'text-gray-400 border-transparent'"
            @click="onSelectTab('id')"
          >
            아이디 찾기
          </button>

          <button
            class="pb-2 text-[17px] font-semibold border-b-2"
            :class="tab === 'pw' ? 'text-blue-600 border-blue-600' : 'text-gray-400 border-transparent'"
            @click="onSelectTab('pw')"
          >
            비밀번호 재설정
          </button>
        </div>
      </div>

      <!-- 아이디 찾기 기본 화면 -->
      <div v-if="tab === 'id' && step === 'input'" class="flex flex-col items-center">
        <div class="mt-10 text-center text-gray-600">등록하신 전화번호를 입력해주세요.</div>

        <div class="mt-6 w-full flex justify-center">
          <input
            v-model="phone"
            type="text"
            placeholder="전화번호 입력(01012345678)"
            class="w-[260px] h-11 px-4 border border-gray-300 rounded-lg text-center text-gray-600 text-[15px] placeholder-gray-400"
          />
        </div>

        <button
          @click="findId"
          class="mt-10 w-[260px] h-12 bg-blue-600 text-white text-[16px] font-semibold rounded-full shadow-sm active:scale-95 transition"
        >
          아이디 찾기
        </button>
      </div>

      <!-- 아이디 찾기 결과 화면 -->
      <div v-if="tab === 'id' && step === 'result'" class="flex flex-col items-center w-full">

        <div class="mt-10 text-gray-600 text-center">
          휴대전화번호 정보와 일치하는 아이디입니다.
        </div>

        <div class="mt-6 w-[340px] border border-gray-300 rounded-xl px-6 py-6">
          <div class="flex items-center mb-4">
            <span class="w-[70px] text-gray-700 font-semibold text-[15px]">아이디 :</span>
            <span class="flex items-center text-[15px] text-gray-800">
              <span
                class="w-5 h-5 flex items-center justify-center rounded bg-green-100 text-green-600 text-[12px] font-bold mr-2"
              >
                N
              </span>
              purus123@naver.com
            </span>
          </div>

          <div class="flex items-center mt-2">
            <span class="w-[70px] text-gray-700 font-semibold text-[15px]">가입일 :</span>
            <span class="text-gray-800 text-[15px]">2025. 11 . 19</span>
          </div>
        </div>

        <div class="flex w-[340px] justify-between mt-10">
          <button
            @click="resetToInput"
            class="w-40 h-12 bg-blue-600 text-white text-[16px] rounded-full font-semibold active:scale-95 transition"
          >
            확인
          </button>

          <button
            @click="tab = 'pw'"
            class="w-40 h-12 border border-gray-400 text-gray-600 text-[16px] rounded-full font-semibold active:scale-95 transition"
          >
            비밀번호 재설정
          </button>
        </div>
      </div>

      <!-- 비밀번호 재설정 기본 화면 -->
      <div v-if="tab === 'pw'" class="flex flex-col items-center w-full">
        <div class="mt-10 text-gray-600 text-center">등록하신 아이디와 전화번호를 입력해주세요.</div>

        <div class="mt-6 w-full flex justify-center">
          <input
            v-model="inputId"
            type="text"
            placeholder="아이디 입력"
            class="w-65 h-11 px-4 border border-gray-300 rounded-lg text-gray-600 text-[15px] placeholder-gray-400"
          />
        </div>

        <div class="mt-3 w-full flex justify-center">
          <input
            v-model="inputPwPhone"
            type="text"
            placeholder="전화번호 입력(01012345678)"
            class="w-65 h-11 px-4 border border-gray-300 rounded-lg text-gray-600 text-[15px] placeholder-gray-400"
          />
        </div>

        <button
          @click="openPwModal"
          class="mt-10 w-65 h-12 bg-blue-600 text-white text-[16px] font-semibold rounded-full shadow-sm active:scale-95 transition"
        >
          비밀번호 재설정
        </button>
      </div>

      <!-- 비밀번호 초기화 완료 모달 -->
      <div
        v-if="modalPw"
        class="absolute top-0 left-0 w-full h-full bg-black/60 backdrop-blur-[1px] flex justify-center items-center"
      >
        <div class="w-[300px] bg-white rounded-2xl py-8 px-6 text-center shadow-lg">

          <div class="flex justify-center mb-4">
            <div class="w-[55px] h-[55px] bg-blue-500 rounded-full flex justify-center items-center">
              <svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" stroke-width="3" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />
              </svg>
            </div>
          </div>

          <div class="font-semibold leading-7 text-gray-800">
            비밀번호가 초기화되었습니다.<br />
            다시 로그인해주세요.
          </div>

        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";   

const router = useRouter();               

const tab = ref("id");
const step = ref("input");

const phone = ref("");
const inputId = ref("");
const inputPwPhone = ref("");

const modalPw = ref(false);

const onSelectTab = (value) => {
  tab.value = value;
  step.value = "input";
};

const findId = () => {
  if (!phone.value) return alert("전화번호를 입력해주세요.");
  step.value = "result";
};

const resetToInput = () => {
  step.value = "input";
};

const openPwModal = () => {
  if (!inputId.value || !inputPwPhone.value) {
    return alert("모든 정보를 입력해주세요.");
  }

  modalPw.value = true;

  // 3초 뒤 모달 닫힌 후 로그인 페이지로 이동
  setTimeout(() => {
    modalPw.value = false;

    // 입력 초기화
    inputId.value = "";
    inputPwPhone.value = "";

    //  로그인 페이지로 이동
    router.push({ name: "LoginWorker" });   
  }, 2000);
};
</script>
