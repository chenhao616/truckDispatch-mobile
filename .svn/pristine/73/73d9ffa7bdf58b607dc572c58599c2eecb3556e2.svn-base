import Vue from "vue";
import App from "@/App";
import router from "@/router"; // api: https://github.com/vuejs/vue-router
import store from "@/store"; // api: https://github.com/vuejs/vuex
import VueCookie from "vue-cookie"; // api: https://github.com/alfhen/vue-cookie
import "@/element-ui"; // api: https://github.com/ElemeFE/element
import "@/icons"; // api: http://www.iconfont.cn/
import "@/element-ui-theme";
import "@/assets/scss/index.scss";
import httpRequest from "@/utils/httpRequest"; // api: https://github.com/axios/axios
import { isAuth } from "@/utils";
import cloneDeep from "lodash/cloneDeep";
import echarts from "echarts";

import "vant/lib/index.css";
import { Tabbar, TabbarItem, Button } from "vant";
Vue.use(Tabbar);
Vue.use(TabbarItem);
Vue.use(Button);

import Print from "vue-print-nb";
Vue.use(Print);

//自定义样式
import "./assets/css/reset.css";
import "./assets/css/style.css";

// 本地 iconfont 字体
import "./assets/font/iconfont/iconfont.css";
import "./assets/font/iconfont/iconfont.ttf";

Vue.use(VueCookie);
Vue.config.productionTip = false;

// 非生产环境, 适配mockjs模拟数据                 // api: https://github.com/nuysoft/Mock
if (process.env.NODE_ENV !== "production") {
  require("@/mock");
}

// 挂载全局
Vue.prototype.$http = httpRequest; // ajax请求方法
Vue.prototype.isAuth = isAuth; // 权限方法
Vue.prototype.$echarts = echarts;

/**
 * 日期格式化
 *
 * @param format 格式化模式串
 * @returns 格式化后字符串
 */
Date.prototype.format2 = function(format) {
  var o = {
    "M+": this.getMonth() + 1, //month
    "d+": this.getDate(), //day
    "h+": this.getHours(), //hour
    "m+": this.getMinutes(), //minute
    "s+": this.getSeconds(), //second
    "q+": Math.floor((this.getMonth() + 3) / 3), //quarter
    "w+": this.getDay(), //week
    S: this.getMilliseconds() //millisecond
  };

  if (/(y+)/.test(format)) {
    format = format.replace(
      RegExp.$1,
      (this.getFullYear() + "").substr(4 - RegExp.$1.length)
    );
  }

  for (var k in o) {
    if (new RegExp("(" + k + ")").test(format)) {
      format = format.replace(
        RegExp.$1,
        RegExp.$1.length == 1 ? o[k] : ("00" + o[k]).substr(("" + o[k]).length)
      );
    }
  }
  return format;
};

Vue.prototype.formatDateYYYYMMDD = function(row, column) {
  const value = row[column.property];
  if (!value) {
    return "";
  }

  let result = "";
  try {
    if (typeof value == "number") {
      result = new Date(value).format2("yyyy-MM-dd");
    } else if (typeof value == "string") {
      let objDate = new Date(Date.parse(value.replace(/-/g, "/"))); //支持IE
      result = objDate.format2("yyyy-MM-dd");
      // result = new Date(Date.parse(value)).format2("yyyy-MM-dd");
    } else {
      result = new Date(Date.parse(value)).format2("yyyy-MM-dd");
    }
  } catch (e) {
    return "";
  }
  return result;
};

Vue.prototype.formatDate = function(value, format) {
  let result = "";
  try {
    if (typeof value == "number") {
      result = new Date(value).format2(format);
    } else if (typeof value == "string") {
      let objDate = new Date(Date.parse(value.replace(/-/g, "/"))); //支持IE
      result = objDate.format2(format);
    } else {
      result = new Date(Date.parse(value)).format2(format);
    }
  } catch (e) {
    return "";
  }
  return result;
};

Vue.prototype.strFormatDate = function(str) {
  return new Date(Date.parse(str.replace(/-/g, "/")));
};

// 保存整站vuex本地储存初始状态
window.SITE_CONFIG["storeState"] = cloneDeep(store.state);

/* eslint-disable no-new */
new Vue({
  el: "#app",
  router,
  store,
  template: "<App/>",
  components: { App }
});
