<template>
  <a class="item" >
    <div class="flex-r">
      <div class="cover">
        <img :src="data.item.doc.cover.small_url" />
      </div>
      <div class="right">
        <div class="title">{{data.item.doc.title}}</div>
        <div class="info">
          <span>{{data.item.doc.category_name}}</span>
          <span class="ml-5">{{data.item.doc.listened_count}}/{{data.item.doc.page_count}}章节</span>
        </div>
        <div class="footer">
          <div class="plan flex-r">
            <div class="plen-view">
              <div class="pn" :style="{'width':pn+'%'}"></div>
            </div>
            <div class="plen-title">已看{{pn}}%</div>
          </div>
          <div class="l-info flex-r">
            <span>上次查看：{{data.item.title}}</span>
            <span>{{data.time}}</span>
          </div>
        </div>
        <div class="btns">
          <button size="mini" @click="go_page(data.item.link)">继续阅读</button>
          <button size="mini" @click="go_doc(data.item.doc.id)">查看文档</button>
        </div>
      </div>
    </div>
  </a>
</template>
<script>
import {navigate} from '../../../utils'
export default {
  props: {
    data: Object
  },
  computed: {
    pn() {
      return parseInt(
        this.data.item.doc.listened_count / this.data.item.doc.page_count * 100
      );
    }
  },
  methods:{
    go_page(link){
      navigate.open_doc_page_info(link)
    },
    go_doc(id){
      navigate.open_doc_index(id)
    }
  }
};
</script>
<style lang="less">
@import "../../../styles/common.less";
@cover-size: 90px;
.item {
  overflow: hidden;
  position: relative;
  padding: 10px 15px;
  .cover {
    width: @cover-size;
    height: @cover-size/0.75;
    margin-right: 15px;
    img {
      width: @cover-size;
      height: @cover-size/0.75;
      border-radius: 2px;
      box-shadow: 2px 2px 8px 0 rgba(0, 0, 0, 0.2);
    }
  }
  .right {
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    .title {
      font-size: 14px;
      line-height: 20px;
      height: 20px;
      overflow: hidden;
      font-weight: bold;
      color: #333;
    }
    .info {
      margin-top: 8px;
      font-size: 10px;
      color: #999;
    }

    .footer {
      margin-top: 5px;
      .plen-view {
        height: 4px;
        flex: 1;
        background: #dcdcdc;
        border-radius: 10px;
        overflow: hidden;
        .pn {
          border-radius: 10px;
          height: 4px;
          background: @blue;
          width: 60%;
        }
      }
      .plen-title {
        font-size: 10px;
        margin-left: 10px;
        color: @blue;
      }
      .l-info {
        margin-top: 8px;
        font-size: 10px;
        color: #999;
        justify-content: space-between;
        span {
          box-sizing: border-box;
          line-height: 15px;
          height: 15px;
          overflow: hidden;
          flex-shrink: 0;
        }
        :first-child {
          margin-right: 15px;
          flex-shrink: 1;
        }
      }
    }
    .btns{
      margin-top: 5px;
      display: flex;
      justify-content: space-between;
      button{
        margin: 0;
      }
    }
  }
}
</style>
