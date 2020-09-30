<template>
  <div class="content">
    <FullCalendar :options="calendarOptions" />

  </div>
</template>

<script>
import FullCalendar from "@fullcalendar/vue";
// import dayGridPlugin from "@fullcalendar/daygrid";
// import interactionPlugin from "@fullcalendar/interaction";
// import resourceTimelinePlugin from "@fullcalendar/resource-timeline";
import timeGridPlugin from "@fullcalendar/timegrid";

import Tooltip from "tooltip.js";

export default {
  components: {
    FullCalendar, // make the <FullCalendar> tag available
  },

  data() {
    return {
      calendarOptions: {
        plugins: [
          timeGridPlugin,
          // resourceTimelinePlugin,
          // dayGridPlugin,
          // interactionPlugin,
        ], //使用插件--------------------------------------------
        initialView: "timeGridDay", //当前视图--------------------------------------------
        locale: "zh-cn", //语言模式--------------------------------------------
        headerToolbar: false, //日历头部工具栏--------------------------------------------
        // dateClick: this.handleDateClick, //点击格子事件--------------------------------------------
        // schedulerLicenseKey: "GPL-My-Project-Is-Open-Source", //调度器许可，不知道收不收钱--------------------------------------------
        eventColor: "#edf2fe", //事件背景颜色--------------------------------------------
        eventTextColor: "#444444", //事件文字颜色-------------------------------------------
        eventBorderColor: "#edf2fe", //事件边框颜色-------------------------------------------
        displayEventTime: true, //事件上是否显示时间文本--------------------------------------------
        displayEventEnd: true, //是否显示事件结束时间--------------------------------------------
        slotEventOverlap: false, //是否会重叠--------------------------------------------
        allDaySlot: false, //是否显示全天--------------------------------------------
        slotDuration: "00:15:00", //一格时间槽代表多长时间，默认00:30:00（30分钟）
        snapDuration: "00:01:00", //拖动事件将捕捉到时间轴的时间间隔。
        slotLabelInterval: "01:00", //左边时间显示间隔1个小时显示
        slotLabelFormat: this.slotLabelFormat, //左边时间--------------------------------------------
        scrollTime: "00:00:00",
        // slotMinTime: "00:00", //开始时间  默认00
        // slotMaxTime: "24:00", //结束时间  默认24
        nowIndicator: true, //是否显示指示当前时间的标记。
        expandRows: true, //如果给定视图的行没有占据整个高度，则它们将扩展以适合。
        navLinks: false, // 是否可以点击表头
        navLinkDayClick: this.navLinkDayClick, //点击表头事件--------------------------------------------
        editable: false, //是否可编辑，即进行可拖动和缩放操作。
        selectable: true, //	是否允许用户通过单击或拖动选择日历中的对象，包括天和时间。
        dayMaxEvents: true, //一天内的事件，过多会以弹窗形式展示
        eventClick: this.eventClick, //点击任务时的点击事件--------------------------------------------
        eventMouseEnter: this.eventMouseEnter, //进入任务时触发--------------------------------------------
        eventMouseLeave: this.eventMouseLeave, //离开任务时触发--------------------------------------------
        dayHeaders: false, //表格头部--------------------------------------------
        eventContent: this.eventContent, //内容事件···································
        eventDidMount: this.eventDidMount, //任务事件挂载后···································
        //数据--------------------------------------------
        events: [
          {
            end: "2020-09-28",
            start: "2020-09-26",
            title: "Conference",
            uuid: "4",
          },
          {
            end: "2020-09-27T12:30:00+00:00",
            start: "2020-09-27T10:30:00+00:00",
            title: "我是",
            // url: "/helloworld", //跳转地址
            data: {
              name: 1,
            },
            uuid: "5",
          },
          {
            start: "2020-09-30T12:00:00+00:00",
            end: "2020-09-30T12:30:00+00:00",
            title: "我不是",
            description: "123465",
            uuid: "3",
          },
          {
            start: "2020-09-30T07:15:00+00:00",
            end: "2020-09-30T12:30:00+00:00",
            title: "我真的是",
            description: "123465",
            uuid: "2",
          },
          {
            start: "2020-09-30T07:15:00+00:00",
            end: "2020-09-30T12:30:00+00:00",
            title: "我真的是什么",
            description: "撒U盾逼真细腻工资就差那山东农萨达",
            uuid: "1",
          },
        ],
      },
    };
  },

  methods: {
    //点击表头的事件--------------------------------------------
    navLinkDayClick(date, jsEvent) {
      console.log(jsEvent);
      console.log("day", date.toISOString());
      console.log("coords", jsEvent.pageX, jsEvent.pageY);
    },

    //点击空格时的点击事件--------------------------------------------
    handleDateClick(e) {
      console.log(e);
    },

    //点击任务时的点击事件--------------------------------------------
    eventClick(event) {
      console.log("eventClick -> event", event);
    },
    //进入任务时触发--------------------------------------------
    eventMouseEnter(info) {
      // console.log("eventMouseEnter -> info", info);
    },
    //离开任务时触发--------------------------------------------
    eventMouseLeave(info) {
      // console.log("eventMouseEnter -> info", info);
    },

    //任务内容组装--------------------------------------------
    eventContent(arg) {
      // let italicEl = document.createElement("i");
      // if (arg.event.extendedProps.isUrgent) {
      //   italicEl.innerHTML = "urgent event";
      // } else {
      //   italicEl.innerHTML = "normal event";
      // }
      // let arrayOfDomNodes = [italicEl];
      // return { domNodes: arrayOfDomNodes };
    },

    //任务事件挂载后--------------------------------------------
    eventDidMount(info) {
      console.log("eventDidMount -> info", info);
      var tooltip = new Tooltip(info.el, {
        title: info.event.extendedProps.description,
        placement: "top",
        trigger: "hover",
        html: true,
      });
    },

    //左边时间字符串--------------------------------------------
    slotLabelFormat(date) {
      let hour = date.date.hour;
      let str = `${hour < 10 ? "0" + hour : hour}:00`;
      return str;
    },
  },
};
</script>


<style lang="scss" scoped>
/deep/ .fc-timegrid-slot-minor {
  border: none;
}

// 鼠标悬浮任务时
/deep/ .fc-timegrid-event-harness {
  &:hover {
    transform: translateY(-1px);
    box-shadow: 0 0 10px 0 rgba($color: #000000, $alpha: 0.1);
    cursor: pointer;
  }
}
</style>


<style>
@import "./css/tooltip.css";
:root {
  /* 当前时间线颜色 */
  --fc-now-indicator-color: skyblue;
  /* 格子背景颜色 */
  --fc-today-bg-color: #fff;
  /* 边框颜色 */
  --fc-border-color: #ebeef5;
}
</style>