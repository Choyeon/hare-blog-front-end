<template>
  <div class="tag">
    <br>
    <Card>
      <p slot="title">
        <Icon type="md-pricetags" color="#fd7792"/>
        标签
      </p>
      <p v-show="loading">
        <Tag class="skeleton-tag" v-for="i in skeleton" :key="i"></Tag>
      </p>
      <div class="wrapper">
        <p v-show="!loading">
          <tag color="primary" v-for="tag in tagList" :key="tag.id">{{tag.name}}</tag>
        </p>
      </div>
    </Card>
  </div>
</template>
<script>
  export default {
    name: "TagCard",
    data() {
      return {
        // 标签列表
        tagList: [],
        skeleton: new Array(10),
        loading: true,
      }
    },
    created() {
      this.axios({
        method: 'get',
        url: 'https://api.choyeon.cn/tag/',
      }).then((response) => {
        this.tagList = response.data
        this.loading = false
      })
    }
  }
</script>

<style scoped>
  .skeleton-tag {
    background: rgb(194, 207, 214);
    width: 40px;
    height: 25px;
    transform-origin: left;
    animation: skeleton-stretch .5s linear infinite alternate;
  }

  @keyframes fade-in {
    0% {
      opacity: 0;
    }
    /*初始状态 透明度为0*/
    40% {
      opacity: 0;
    }
    /*过渡状态 透明度为0*/
    100% {
      opacity: 1;
    }
    /*结束状态 透明度为1*/
  }

  @-webkit-keyframes fade-in { /*针对webkit内核*/
    0% {
      opacity: 0;
    }
    40% {
      opacity: 0;
    }
    100% {
      opacity: 1;
    }
  }

  .wrapper {
    animation: fade-in; /*动画名称*/
    animation-duration: .6s; /*动画持续时间*/
    -webkit-animation: fade-in .6s; /*针对webkit内核*/
  }

</style>
