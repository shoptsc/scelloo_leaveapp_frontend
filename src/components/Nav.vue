<template>
  <div>
    <div class="block md:flex w-full h-12 bg-white">
      <span @click="showMenu()" class="cursor-pointer">
        <i class="fa fa-bars text-gray-400 px-2 md:px-6 py-4"></i>
      </span>
      <div class="absolute top-3 left-10 md:left-1/4 w-6/12">
        <img
          src="../assets/images/magnifying-glass.png"
          class="search absolute left-3 top-1/4 w-15 h-15"
          alt=""
        />

        <input
          type="text"
          class="px-10 bg-gray-300 rounded outline-none w-9/12 md:w-10/12 text-white"
          placeholder="Search"
        />
      </div>
      <div
        class="absolute top-2.5 bg-white right-28 md:right-40
    border-2 border-gray-300 px-2 md:px-5 rounded text-gray-300 float-right"
      >
        <small>Scelloo</small>
      </div>
      <div>
        <img
          class="absolute float-right top-3 right-20 md:right-28 px-2 md:px-3"
          src="../assets/images/bell.png"
          alt=""
        />
        <img
          class="absolute float-right top-3 right-16 md:right-24 px-1 "
          src="../assets/images/gear.png"
          alt=""
        />

        <span
          class="absolute float-right top-3 right-16 md:right-20 px-0 md:px-3"
          ><i class="fa fa-th absolute text-gray-400" aria-hidden="true"></i
        ></span>
        <img
          class="absolute float-right top-1 right-2 md:right-3 px-0 md:px-3"
          src="../assets/images/African-american-man.png"
          alt="African man"
        />
      </div>
    </div>
  </div>
</template>

<script>
import { bus } from "../main";
export default {
  components: {},
  data() {
    return {
      open: false,
    };
  },
  methods: {
    showMenu() {
      this.open = !this.open;
      bus.$emit("openMenu", "trying");
    },
  },
};
</script>

<style></style>
