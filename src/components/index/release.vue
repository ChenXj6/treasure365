<template>
  <div>
    <div>
      <van-nav-bar :title="$t('m.Announcement.News')" left-text left-arrow @click-left="onClickLeft" />
    </div>
    <div class="p20">
      <div class="releaselist" v-for="(item,index) in newlist" :key="index" @click="detail(item.id)">
        <p>{{item.title}}</p>
        <!-- <p v-html="item.detail"> -->
        <!-- </p> -->
        <!-- <p class="mt2 times">{{item.createtime}}</p> -->
      </div>
    </div>
  </div>
</template>

<script>
export default {
    data(){
        return{
            page:1,
            newlist:''
        }
    },
    mounted(){
       this.news()
    },
  methods: {
    onClickLeft() {
     this.$router.go(-1)
    },
    detail(e){
        this.$router.push({name:'detail',query:{id:e}})
    },
    news(){
        this.$api.Post('news',{page:this.page}).then(res=>{
            if(res.status==1){
                this.newlist=res.result.news;
            }
      })
    }
  }
};
</script>

<style lang="less">
.releaselist {
  box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24) !important;
  transition: all 0.3s cubic-bezier(.25,.8,.25,1);
}
.releaselist:hover {
  box-shadow: 0 14px 28px rgba(0,0,0,0.25), 0 10px 10px rgba(0,0,0,0.22) !important;
}
.releaselist {
  padding: 15px;
  margin-bottom: 15px;
  border-radius: 4px;
  background-color: #1e243d;
  > p:nth-child(1) {
    font-weight: 700;
  }
  > p:nth-child(2) {
    margin-top: 20px;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 3;
    -webkit-box-orient: vertical;
    text-align: justify;
    color: #5d70bd !important;
  }
  .times{
      color: rgba(0, 0, 0, 0.3);
      font-size: 14px;
  }
}
</style>