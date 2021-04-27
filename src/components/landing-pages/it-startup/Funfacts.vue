<template>
  <!-- Start Fun Facts Area -->
  <section class="funfacts-area ptb-80 pt-0">
    <div class="container">
      <div class="contact-cta-box">
        <h3>
          কেনার আগে ব্যবহার করে দেখতে চান ?
          ৭ দিনের ফ্রি ট্রায়াল নিতে পাশের কোড টি ব্যবহার করুন
        </h3>
      
          <span class="btn btn-primary" id="message"  v-clipboard:copy="message"
            v-clipboard:success="onCopy"
            v-clipboard:error="onError">{{message}}</span>
            <span class="test" v-clipboard:copy="message"
            v-clipboard:success="onCopy"
            v-clipboard:error="onError">Click for copy</span>
       
      </div>

      <div class="map-bg">
        <img src="../../../assets/img/map.png" alt="map" />
      </div>
    </div>
  </section>
  <!-- End Fun Facts Area -->
</template>

<script>
import "odometer/themes/odometer-theme-default.css";

export default {
  name: "Funfacts",
  data() {
    return {
      contributors: 111,
      workers: 70,
      feedback: 8,
      downloaded: 10,
      message: "trial",
    };
  },
  mounted() {
    const that = this;
    setInterval(function () {
      that.contributors += 1;
    }, 3000);
    setInterval(function () {
      that.workers += 1;
    }, 5000);
    setInterval(function () {
      that.feedback += 1;
    }, 2000);
    setInterval(function () {
      that.downloaded += 1;
    }, 1000);
  },
  methods: {
    onCopy: function (e) {
      alert("Copy Successfull: " + e.text);
    },
    onError: function (e) {
      alert("Failed to copy the text to the clipboard");
      console.log(e);
    },
  },
};
</script>


<style scoped>
.test{
  position: absolute;
  right: 5%;
  cursor: pointer;
}
</style>