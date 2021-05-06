<template>
  <div class="main bg-blue-700 sm:flex sm:items-center text-white w-20">
    <router-link to="#"
      ><img
        class="absolute top-36 sm:top-28 left-5"
        src="../assets/images/img1.png"
        alt=""
    /></router-link>
    <router-link to="#"
      ><img
        class="absolute top-48 sm:top-40 left-5"
        src="../assets/images/img2.png"
        alt=""
    /></router-link>

    <router-link to="#"
      ><i
        class="fa fa-credit-card absolute top-60 sm:top-52 left-5"
        aria-hidden="true"
      ></i
    ></router-link>
    <router-link to="/absencehistory"
      ><i
        class="bg-blue-500 pl-5 pr-10 py-2 fa fa-american-sign-language-interpreting absolute top-72 sm:top-64 left-0"
      ></i
    ></router-link>
    <i class="fa fa-calendar-check absolute bottom-72 left-5"></i>
    <i class="fa fa-handshake absolute bottom-56 left-5"></i>
    <router-link to="#"
      ><img
        class="absolute bottom-44 left-5"
        src="../assets/images/img4.png"
        alt=""
    /></router-link>
    <router-link to="#"
      ><img
        class="absolute bottom-32 left-5"
        src="../assets/images/img5.png"
        alt=""
    /></router-link>
    <router-link to="#"
      ><img
        class="absolute bottom-16 left-5"
        src="../assets/images/img6.png"
        alt=""
    /></router-link>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.main {
  min-height: 100vh;
}
</style>
