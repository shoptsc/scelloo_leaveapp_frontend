<template>
  <!-- component -->
  <form
    @submit.prevent="submitLeave"
    v-if="showModal"
    class="overflow-x-hidden h-11/12 py-10 fixed inset-0 outline-none focus:outline-none flex justify-center items-center bg-transparent antialiased z-10"
  >
    <div
      class="flex flex-col w-11/12 sm:w-5/6 lg:w-1/2 max-w-2xl mx-auto rounded-lg border overflow-y-auto  transform transition-all transition-opacity border-gray-300 bg-gray-100 shadow-xl h-5/6"
    >
      <div
        class="flex flex-row justify-between p-6 bg-gray-100 border-b border-gray-200 rounded-tl-lg rounded-tr-lg"
      >
        <p class="font-semibold text-gray-800">Request Leave</p>
        <button v-on:click="toggleModal()">
          <svg
            class="w-6 h-6"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M6 18L18 6M6 6l12 12"
            ></path>
          </svg>
        </button>
      </div>
      <div class="flex flex-col px-6 py-5 bg-gray-50">
        <div class="flex flex-col sm:flex-row items-center mb-5 sm:space-x-5">
          <div class="w-full sm:w-1/2 ">
            <p class="mb-2 font-semibold text-gray-700">Leave Type</p>
            <select
              type="text"
              name=""
              class="w-full px-5 py-2 bg-gray-100 border border-gray-200 rounded shadow-sm outline-none"
              v-model="leave"
            >
              <option v-for="(leave, index) of leaves" :key="index">{{
                leave
              }}</option>
            </select>
          </div>
          <div class="w-full sm:w-1/2 mt-2 sm:mt-0">
            <p class="mb-2 font-semibold text-gray-700">Details</p>
            <input
              type="text"
              name=""
              v-model="details"
              class="w-full px-5 py-2 bg-gray-100 border border-gray-200 rounded shadow-sm outline-none"
              placeholder="Exams"
            />
          </div>
        </div>
        <div class="flex flex-col sm:flex-row items-center mb-5 sm:space-x-5">
          <div class="w-full sm:w-1/2">
            <p class="mb-2 font-semibold text-gray-700">Duration</p>
            <div class="bg-gray-100">
              <Datepicker
                class="rounded bg-gray-100 w-4/12 border-2 "
                name="Start Date"
                v-model="startDate"
                :format="DatePickerFormat"
                :disabled-dates="disabledStartDates"
              />
              <p>To</p>
              <Datepicker
                class="rounded bg-gray-100 w-4/12 border-2"
                name="End Date"
                v-model="endDate"
                :format="DatePickerFormat"
                :disabled-dates="disabledStartDates"
              />
            </div>
          </div>
          <div class="w-full sm:w-1/2 mt-2 sm:mt-0">
            <p class="mb-2 font-semibold text-gray-700">Days Requested</p>
            <p class="font-semibold text-gray-700">{{ duration }}</p>
          </div>
        </div>
        <div class="flex flex-col sm:flex-row items-center mb-5 sm:space-x-5">
          <div class="w-full sm:w-1/2">
            <p class="mb-2 font-semibold text-gray-700">Leave Allowance</p>
            <select
              v-model="allowance"
              type="text"
              name=""
              class="w-full px-5 py-2 bg-gray-100 border border-gray-200 rounded shadow-sm outline-none"
              id=""
            >
              <option
                v-for="(allowance, index) of allowances"
                :key="index"
                v-bind:value="allowance"
                >{{ allowance }}</option
              >
            </select>
          </div>
          <div class="relative w-full sm:w-1/2 mt-2 sm:mt-0">
            <p class="mb-2 font-semibold text-gray-700">Delegates</p>
            <span class="absolute top-10 left-4"
              ><i class="fa fa-search text-gray-400"></i
            ></span>
            <input
              type="text"
              class=" w-full px-10 py-2 bg-gray-100 border border-gray-200 rounded shadow-sm outline-none"
              placeholder="Chuwudi Abayomi"
              v-model="delegate"
            />
          </div>
          <!-- <div v-for="(delegate, index) of filterDelegate" :key="index"> -->
          <!-- <p>{{ delegate.name }}</p> -->
          <!-- </div> -->
        </div>

        <div
          class="flex flex-row items-center justify-between p-2 bg-white border border-gray-200 rounded shadow-sm sm:w-72 sm:absolute -bottom-5 right-8"
        >
          <div class=" flex flex-row items-center">
            <img
              class="w-10 h-10 mr-3 rounded-full "
              src="../assets/images/African-american-man.png"
              alt=""
            />
            <div class="flex flex-col">
              <p class="font-semibold text-gray-800">Chukwudi Abayomi</p>
              <p class="text-gray-400">chukwudi@testcompany.com</p>
            </div>
          </div>
        </div>
      </div>
      <div class="mx-5 sm:mt-10">
        <p>
          By Submitting, You confirm that you have read and agreed to the terms
          and conditions of the Leave requests. Click
          <router-link class="text-blue-700" to="/">here</router-link> to read.
        </p>
      </div>
      <div
        class="flex flex-row items-center justify-between p-5 bg-gray-100 border-t border-gray-200 rounded-bl-lg rounded-br-lg"
      >
        <button class="px-4 py-2 text-white font-semibold bg-blue-500 rounded">
          Save
        </button>
      </div>
    </div>
  </form>
</template>

<script>
import axios from "axios";
import { bus } from "../main";
import Datepicker from "vuejs-datepicker";
export default {
  data() {
    return {
      showModal: false,
      details: "",
      startDate: "",
      endDate: "",
      duration: "",
      DatePickerFormat: "dd/MM/yyyy",
      disabledStartDates: {
        to: new Date(Date.now() - 8640000),
      },
      leave: "",
      allowance: "",
      leaves: [
        "Study Leave",
        "Annual Leave",
        "Unpaid Leave",
        "Compassionate Leave",
        "Sick Leave",
        "Birth Leave",
      ],
      allowances: ["Yes", "No"],
      searchDelegate: "",
      delegate: "",
    };
  },
  components: {
    Datepicker,
  },
  created() {
    bus.$on("openModal", () => {
      this.showModal = !this.showModal;
    });
  },
  methods: {
    toggleModal: function() {
      this.showModal = !this.showModal;
    },
    async submitLeave() {
      const url = "https://scelloo-leaveapp.herokuapp.com/user/leave";
      const datas = {
        leave: this.leave,
        details: this.details,
        days: this.duration,
        start: this.startDate,
        end: this.endDate,
        allowance: this.allowance,
        delegate: this.delegate,
      };
      await axios
        .post(url, datas)
        .then(() => {
          this.toggleModal();
          this.$router.push("/absencehistory").catch(() => {});
        })

        .catch((err) => console.log(err));
    },
  },
  computed: {
    // filterDelegate() {
    //   return this.delegates.filter((delegate) => {
    //     return delegate.name.match(this.searchDelegate);
    //   });
    // },
  },

  updated() {
    this.duration =
      Math.round(this.endDate / 86400000) -
      Math.floor(this.startDate / 86400000);
  },
};
</script>
