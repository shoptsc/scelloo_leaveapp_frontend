<template>
  <div class="home">
    <Nav />
    <div class="flex main">
      <SideNav :class="open ? 'block' : 'hidden'" />
      <div class=" flex-1 ">
        <div class="pt-5">
          <p class="float-left mx-5 md:mx-12 font-mono">Leave</p>
          <button
            v-on:click="toggleModal()"
            class="float-right text-sm bg-blue-700 text-white px-2 py-1 mx-5 md:mx-12 rounded"
          >
            New Request
          </button>
          <Modal />
        </div>
        <div class="bg-white w-11/12  mx-auto my-16 p-5 rounded">
          <div class="w-11/12 md:w-5/12 mx-auto py-5">
            <img class="mx-auto" src="../assets/images/Group11292.png" alt="" />
            <p class="text-center pt-6 font-sans">
              You have not made any Leave request. Click on the New Request
              button to make a leave request
            </p>
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
import Modal from "../components/Modal";
import { bus } from "../main";

export default {
  data() {
    return {
      open: false,
    };
  },
  name: "Home",
  components: {
    Nav,
    SideNav,
    Footer,
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
.home {
  background: #e5e5e5;
  width: 100%;
}
.main {
  height: 100vh;
}
</style>
