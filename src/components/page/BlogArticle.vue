<template>
    <div class="article" align="left">
        <article v-for="item in articleList" :key="item.id">

            <!-- 文章标题 -->
            <header>
                <h3>{{item.title}}</h3>
                <em>{{item.date}}</em>
            </header>

            <!-- 文章内容 -->
            <p>
                {{item.content}}
            </p>

            <!-- 查看更多 -->
            <div align="center" class="more">
               <svg class="icon" aria-hidden="true">
                  <use xlink:href="#icon-arrow"></use>
                </svg>
            </div>

            <!-- 分割线 -->
            <div class="line"></div>

            <!-- 文章底部功能 -->
            <footer>
                <div>
                  <svg class="icon" aria-hidden="true">
                    <use xlink:href="#icon-zhuanfa"></use>
                  </svg>
                </div>
                <div>
                  <svg class="icon" aria-hidden="true">
                    <use xlink:href="#icon-xihuan"></use>
                  </svg>
                </div>
                <div>
                  <svg class="icon" aria-hidden="true">
                    <use xlink:href="#icon-pinglun"></use>
                  </svg>
                </div>
            </footer>
        </article>
    </div>
</template>

<script>
    export default {
        name: "BlogArticle",
        data() {
            return {
                articleList: []
            }
        },
        methods: {
          getData() {
            this.$axios.get(this.$api.getArticleData).then((result) => {
              console.log(result);
              this.articleList = result.data;
            }).catch((err) => {
              console.log(err);

            });
          }
        },
        created () {
          this.getData();
        }
    }
</script>

<style scoped>

    /* 图标样式 */
    .icon {
      color: #333;
    }
    .article>article:first-child{
       margin-top: 0;
    }
    .article>article{
        margin-top: 20px;
        background-color: #fff;
        box-sizing: border-box;
        padding: 30px;
        box-shadow: 0 3px 3px rgba(128, 128, 128, .3);
    }
    .article h3{
        display: inline-block;
        margin-right: 30px;
    }
    .article p,.article footer{
        margin-top: 30px;
    }
    .article footer{
        display: flex;
        flex-flow: row-reverse nowrap;

    }
    .article footer>div{
        margin-left: 15px;
        padding-left: 15px;
        border-left: 1px solid gray;
    }
    .article footer>div:last-child{
        border-left: none;
    }

    .more{
      margin-top: 30px;
    }

    .more .icon{
      color: rgba(128, 128, 128, .3);
    }

    .line{
      margin: 20px 0;
      width: 100%;
      height: 1px;
      background-color: rgba(128, 128, 128, .3);
      position: relative;
    }
</style>
