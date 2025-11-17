<template>
  <div class="w-full flex justify-center bg-white">

    <!-- 모바일 고정 레이아웃 -->
    <div class="w-full max-w-[390px] min-h-screen bg-white flex flex-col items-center pb-16">

      <!-- 상단 바 -->
      <div class="w-full flex items-center justify-between px-5 py-4 border-b border-gray-200">
        <i class="fa-solid fa-house text-xl"></i>

        <div class="relative">
          <i class="fa-regular fa-bell text-xl"></i>
          <span
            class="absolute -top-1 -right-2 bg-red-500 text-white text-[10px] w-4 h-4 flex items-center justify-center rounded-full"
          >
            20
          </span>
        </div>
      </div>

      <!-- 프로필 이미지 -->
      <div class="mt-8 flex flex-col items-center">
        <img
          src="/public/images/Editinfo.png"
          class="w-36 h-36 rounded-xl object-cover"
          alt="profile"
        />

        <button
          class="mt-4 border border-gray-300 text-gray-600 text-[] px-4 py-1 rounded-full"
        >
          사진변경
        </button>
      </div>

      <!-- 정보 리스트 -->
      <div class="w-full mt-10 px-6 text-[15px]">

        <div class="flex items-center justify-between py-3.5 border-b">
          <span class="text-gray-500">이름</span>
          <div class="flex items-center space-x-3">
            <span class="text-black">이깨끗</span>
            <i class="fa-solid fa-chevron-right text-[#555555] text-xs"></i>
          </div>
        </div>

        <div class="flex items-center justify-between py-3.5 border-b">
          <span class="text-gray-500">생년월일</span>
          <div class="flex items-center space-x-3">
            <span class="text-black">1988.12.25</span>
            <i class="fa-solid fa-chevron-right text-[#555555] text-xs"></i>
          </div>
        </div>

        <div class="flex items-center justify-between py-3.5 border-b">
          <span class="text-gray-500">휴대폰 번호</span>
          <div class="flex items-center space-x-3">
            <span class="text-black">010-1234-5678</span>
            <i class="fa-solid fa-chevron-right text-[#555555] text-xs"></i>
          </div>
        </div>

        <div class="flex items-center justify-between py-3.5 border-b">
          <span class="text-gray-500">이메일</span>
          <div class="flex items-center space-x-3">
            <span class="text-black">clean1004@naver.com</span>
            <i class="fa-solid fa-chevron-right text-[#555555] text-xs"></i>
          </div>
        </div>

        <div class="flex items-center justify-between py-3.5 border-b">
          <span class="text-gray-500">주소</span>
          <div class="flex items-center space-x-3">
            <span class="text-black">대구시 수성구 수성대로111</span>
            <i class="fa-solid fa-chevron-right text-[#555555] text-xs"></i>
          </div>
        </div>

        <div class="flex items-center justify-between py-3.5 border-b">
          <span class="text-gray-500">비밀번호</span>
          <div class="flex items-center space-x-3">
            <span class="text-black">*******</span>
            <i class="fa-solid fa-chevron-right text-[#555555] text-xs"></i>
          </div>
        </div>
      </div>

      <!-- 저장 btn-->
      <div class="w-full px-6 mt-10">
        <button class="w-full bg-blue-600 text-white py-3.5 rounded-full text-[16px]">
          저장하기
        </button>
      </div>

    </div>
  </div>
</template>

<script setup>
</script>