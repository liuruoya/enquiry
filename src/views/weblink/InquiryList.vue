<!--询价单列表-->
<template>
  <PageModel :icon-src="icon_bidding" title-name="询价公告">
    <FilterInput slot="head-right" @filter="doFilter"></FilterInput>
    <el-container id="el-container">
      <el-main>
        <el-row class="bidding-item-normal" v-for="item in biddingList" :key="item.id">
          <el-row id="bidding-name">
            <el-link href="#" target="_blank" class="link">
              {{ item.name }}
            </el-link>
          </el-row>
          <el-row id="bidding-date">
            <div class="date">
              <span>发布时间：<span class="time">{{ item.star }}</span></span>
              <span style="margin-left: 20px">截止时间：<span class="time">{{ item.end }}</span></span>
            </div>
          </el-row>
        </el-row>
      </el-main>
      <el-footer>
        <el-row style="margin: 30px 0">
          <Page :total="pager.total" :limit="pager.limit" @changePage="getPage"></Page>
        </el-row>
      </el-footer>
    </el-container>
  </PageModel>
</template>

<script>
import PageModel from '../../components/PageModel'
import Page from '../../components/Page'
import FilterInput from '../../components/FilterInput'
// 测试用数据
import dataList from '../../../static/data/InquiryList'

export default {
  name: 'InquiryList',
  components: { PageModel, FilterInput, Page },
  data () {
    return {
      icon_bidding: '../../static/img/icon_bidding.png',
      inputFilter: '',
      biddingList: [],
      pager: {
        total: 0,
        page: 1,
        limit: 10
      }
    }
  },
  methods: {
    doFilter (input) {
      this.pager.page = 1
      this.inputFilter = input
      this.getData(this.inputFilter, 1, this.pager.limit)
      alert(input)
    },
    getPage (page) {
      this.pager.page = page
      this.getData(this.inputFilter, page, this.pager.limit)
    },
    getData (filter, page, limit) {
      this.biddingList = dataList.data
      this.pager.total = dataList.count
      console.log(this.tableData)
    }
  },
  created () {
    this.getData(this.inputFilter, this.pager.page, this.pager.limit)
  }
}
</script>

<style scoped>
  .bidding-item-normal {
    border: 1px;
    border-bottom: 1px dashed #dedede /*solid rgba(0, 17, 59, 0.05)*/;
    overflow: hidden;
    height: 100px;
  }

  #bidding-name {
    margin-top: 30px;
    /*width: 397px;*/
    height: 21px;
    font-size: 16px;
    font-family: Microsoft YaHei, Microsoft YaHei-Regular;
    font-weight: 400;
    text-align: left;
    color: #333333;
    line-height: 24px;
  }

  .link {
  }

  #bidding-date {
    height: 16px;
    font-size: 12px;
    font-family: Microsoft YaHei, Microsoft YaHei-Regular;
    font-weight: 400;
    text-align: left;
    color: #999999;
    line-height: 24px;
    margin: 10px 0;
  }

  .time {
    height: 16px;
    font-size: 12px;
    font-family: Microsoft YaHei, Microsoft YaHei-Regular;
    font-weight: 400;
    text-align: left;
    color: #0096c3;
    line-height: 24px;
  }

  #el-container .el-main {
    padding: 0;
  }
</style>
