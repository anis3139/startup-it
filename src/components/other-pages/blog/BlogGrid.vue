<template>
  <div>
    <!-- Start Page Title -->
    <div class="page-title-area">
      <div class="d-table">
        <div class="d-table-cell">
          <div class="container">
            <h2>Blog Grid</h2>
          </div>
        </div>
      </div>

      <div class="shape1">
        <img src="../../../assets/img/shape1.png" alt="shape" />
      </div>
      <div class="shape2 rotateme">
        <img src="../../../assets/img/shape2.svg" alt="shape" />
      </div>
      <div class="shape3">
        <img src="../../../assets/img/shape3.svg" alt="shape" />
      </div>
      <div class="shape4">
        <img src="../../../assets/img/shape4.svg" alt="shape" />
      </div>
      <div class="shape5">
        <img src="../../../assets/img/shape5.png" alt="shape" />
      </div>
      <div class="shape6 rotateme">
        <img src="../../../assets/img/shape4.svg" alt="shape" />
      </div>
      <div class="shape7">
        <img src="../../../assets/img/shape4.svg" alt="shape" />
      </div>
      <div class="shape8 rotateme">
        <img src="../../../assets/img/shape2.svg" alt="shape" />
      </div>
    </div>
    <!-- End Page Title -->

    <!-- Start Blog Area -->
    <section class="blog-area ptb-80">
      <div class="container">
        <div class="row">
          <div class="col-lg-4 col-md-6" v-for="allNews of allNewses" :key="allNews.id">
            <div class="single-blog-post">
              <div class="blog-image">
                <a href="#">
                  <img :src=" allNews.image" alt="image" />
                </a>

                <div class="date">
                  <feather type="calendar"></feather>
                  {{ moment(allNews.publishDate).format('Do-MMM-YYYY') }}
                </div>
              </div>

              <div class="blog-post-content">
                <h3>
                  <a href="#">{{ allNews.title }}</a>
                </h3>

                <span>
                  by
                  <a href="#">{{ allNews.published_by }}</a>
                </span>

                <p>{{ allNews.description.substring(0,200)+"..." }}</p>

                <a href="#" class="read-more-btn">
                  Read More
                  <feather type="arrow-right"></feather>
                </a>
              </div>
            </div>
          </div>

          <div class="col-lg-12 col-md-12">
            <div class="pagination-area">
              <nav aria-label="Page navigation">
                <jw-pagination :items="pageOfItems" @changePage="onChangePage" :pageSize="9"></jw-pagination>
              </nav>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- End Blog Area -->
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "BlogGrid",
  data() {
    return {
      errors: [],
      allNewses: [],
      pageOfItems: [],
    };
  },

  mounted() {
    axios
      .get("api/v1/news/all")
      .then((response) => {
        this.pageOfItems = response.data.data;
      })
      .catch((error) => {
        this.errors.push(error);
      });
  },

  methods: {
    onChangePage(pageOfItems) {
      console.log(pageOfItems);
      this.allNewses = pageOfItems;
    },
  },
};
</script>