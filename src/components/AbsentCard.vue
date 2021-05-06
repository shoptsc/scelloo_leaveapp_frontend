<template>
  <div>
    <div class=" m-auto hidden md:block font-sans">
      <div
        class="text-center font-bold md:grid grid-cols-8 gap-x-2  py-4 rounded"
      >
        <p class="pl-5 w-40">Leave Type</p>
        <p class="w-40">Details</p>
        <p class="w-40">Start Date</p>
        <p class="w-40">End Date</p>
        <p class="w-40">Duration (Days)</p>
        <p class="pl-5 w-52">Allowance Requested</p>
        <p class="pl-20 w-40">Delegates</p>
        <p></p>
      </div>

      <div
        v-for="(leaves, index) of leaveDetails"
        :key="index"
        class="bg-white text-center  block md:grid grid-cols-8 gap-x-2 block md:py-4 my-2 rounded"
      >
        <p class="pl-5 w-40">{{ leaves.leave }}</p>
        <p class="w-40">{{ leaves.details }}</p>
        <p class="w-40">{{ leaves.start.slice(0, 10) }}</p>
        <p class="w-40">{{ leaves.end.slice(0, 10) }}</p>
        <p class="w-40">{{ leaves.days }}</p>
        <p class="pl-5 w-40">{{ leaves.allowance }}</p>
        <p class="pl-20 w-40">{{ leaves.delegate }}</p>
        <p class="w-40"><i class="fa fa-ellipsis-v" aria-hidden="true"></i></p>
      </div>
    </div>

    <div
      v-for="(leaves, index) of leaveDetails"
      :key="index"
      class="mx-auto block md:hidden bg-white rounded my-5 p-5 font-sans"
    >
      <p class="p-1"><strong>Leave Type :</strong> {{ leaves.leave }}</p>
      <p class="p-1"><strong>Details :</strong> {{ leaves.details }}</p>
      <p class="p-1">
        <strong>Start Date :</strong> {{ leaves.start.slice(0, 10) }}
      </p>
      <p class="p-1">
        <strong>End Date :</strong> {{ leaves.end.slice(0, 10) }}
      </p>
      <p class="p-1"><strong>Duration (Days) :</strong> {{ leaves.days }}</p>
      <p class="p-1">
        <strong>Allowance Requested :</strong> {{ leaves.allowance }}
      </p>
      <p class="p-1"><strong>Delegates :</strong> {{ leaves.delegate }}</p>
      <p class="p-1"><i class="fa fa-ellipsis-h" aria-hidden="true"></i></p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      leaveDetails: [],
      url: "https://scelloo-leaveapp.herokuapp.com/user/leave",
    };
  },
  methods: {
    async leaveData() {
      await axios
        .get(this.url)
        .then((res) => {
          this.leaveDetails = res.data.leaveDetails;
        })
        .catch((err) => console.log(err));
    },
  },
  created() {
    this.leaveData();
  },
  updated() {
    this.leaveData();
  },
};
</script>

<style></style>
