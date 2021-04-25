<template>
    <div class="col-lg-4 col-md-12">
            <aside class="widget-area" id="secondary">
              <section class="widget widget_search">
                <form class="search-form">
                  <label>
                    <span class="screen-reader-text">Search for:</span>
                    <input type="search" class="search-field" placeholder="Search..." />
                  </label>
                  <button type="submit">
                    <feather type="search"></feather>
                  </button>
                </form>
              </section>

              <section class="widget widget_startp_posts_thumb">
                <h3 class="widget-title">Latest Posts</h3>

                <article class="item" v-for="news of newsAll" :key="news.id">
                  <a href="#" class="thumb">
                    <span class="fullimage cover" role="img" :style='{ backgroundImage: `url("${news.image}")` }'></span>
                  </a>
                  <div class="info">
                    <time datetime="2019-06-30"> {{ moment(news.publishDate).format('Do-MMM-YYYY') }}</time>
                    <h4 class="title usmall">
                      <router-link
                    :to="{
                      name: 'blog-details',
                      params: { id: news.id },
                    }"
                  >{{ news.title.substring(0,50)+"..."  }}</router-link>
                    
                    </h4>
                  </div>

                  <div class="clear"></div>
                </article>

               

                
              </section>

              <section class="widget widget_categories">
                <h3 class="widget-title">Categories</h3>

                <ul>
                  <li v-for="cat of cats" :key="cat.id">
                    <a href="#">{{ cat.nameBn }}</a>
                  </li>
                  
                </ul>
              </section>

              <!-- <section class="widget widget_archive">
                <h3 class="widget-title">Archives</h3>

                <ul>
                  <li>
                    <a href="#">May 2019</a>
                  </li>
                  <li>
                    <a href="#">April 2019</a>
                  </li>
                  <li>
                    <a href="#">June 2019</a>
                  </li>
                </ul>
              </section> -->

              <!-- <section class="widget widget_meta">
                <h3 class="widget-title">Meta</h3>

                <ul>
                  <li>
                    <a href="#">Log in</a>
                  </li>
                  <li>
                    <a href="#">
                      Entries
                      <abbr title="Really Simple Syndication">RSS</abbr>
                    </a>
                  </li>
                  <li>
                    <a href="#">
                      Comments
                      <abbr title="Really Simple Syndication">RSS</abbr>
                    </a>
                  </li>
                  <li>
                    <a href="#">WordPress.org</a>
                  </li>
                </ul>
              </section> -->

              <section class="widget widget_tag_cloud">
                <h3 class="widget-title">Tags</h3>

                <div class="tagcloud">
                  <a href="#" v-for="allTag of tagAll" :key="allTag.id">
                    {{ allTag.nameBn }}
                    <!-- <span class="tag-link-count">(3)</span> -->
                  </a>
                 
                </div>
              </section>
            </aside>
          </div>
</template>

<script>
export default {
    name: "SingleSidebar",
     data() {
    return {
      errors: [],
      errorsCat: [],
      errorstagAll: [],
      errorsNews: [],
      title: "",
      image:'',
      description:'',
      publishDateBn:'',
      published_by:'',
      tags:'',
      cats:[],
      tagAll:[],
      newsAll:[],
    };
  },
  mounted() {
    this.getData();
    this.getCatData();
    this.getTagData();
    axios
      .get("api/v1/news/book/recent/all")
      .then((response) => {
        this.newsAll = response.data.data;
        console.log(response.data.data);
      })
      .catch((error) => {
        this.errorsNews.push(error);
      });
  },

}
</script>