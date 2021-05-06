<template>
  <div class="absence  w-full">
    <Nav />
    <div class="flex w-full h-3/4">
      <SideNav :class="open ? 'block' : 'hidden'" />
      <div class=" flex-1 w-3/4 sm:w-full">
        <div class="pt-5 pb-16">
          <div class="float-left mx-5 md:mx-12 ">
            <p class="font-mono font-bold ">Absence History</p>
            <p class="text-sm py-5 md:py-10">
              <router-link to="/" class="text-blue-700 ">Leave ></router-link>
              Absense History
            </p>
          </div>
          <button
            v-on:click="toggleModal()"
            class="float-right text-sm bg-blue-700 text-white px-2 py-1 mx-5 md:mx-12 rounded"
          >
            New Request
          </button>
          <Modal />
        </div>
        <div class="mx-auto my-12 md:my-24">
          <div class="flex md:block md:float-left my-0 md:my-12  py-5 px-8">
            <p class="px-4 md:px-0 py-2 text-blue-700 cursor-pointer">
              Pending
            </p>
            <p class="px-4 md:px-0 py-2 text-gray-700 cursor-pointer">
              Approved
            </p>
            <p class="px-4 md:px-0 py-2 text-gray-700 cursor-pointer">
              Disapproved
            </p>
          </div>
          <div class="w-full mx-auto md:w-10/12 mr-0 md:mr-10 rounded">
            <AbsentCard />
          </div>
        </div>
      </div>
    </div>

    <Footer />
  </div>
</template>

<script>
// @ is an alias to /src
import Nav from "../components/Nav";
import SideNav from "../components/SideNav";
import Footer from "../components/Footer";
import AbsentCard from "../components/AbsentCard.vue";
import { bus } from "../main";
import Modal from "../components/Modal";

export default {
  name: "Home",
  data() {
    return {
      open: false,
    };
  },
  components: {
    Nav,
    SideNav,
    Footer,
    AbsentCard,
    Modal,
  },
  created() {
    bus.$on("openMenu", () => {
      this.open = !this.open;
    });
  },
  methods: {
    toggleModal: function() {
      this.showModal = !this.showModal;
      bus.$emit("openModal", "modal");
    },
  },
};
</script>

<style scoped>
.absence {
  background: #e5e5e5;
  width: 100%;
  min-height: 100vh;
}
</style>
