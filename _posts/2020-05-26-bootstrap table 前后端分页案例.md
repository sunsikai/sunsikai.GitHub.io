---
layout:     post                    # 使用的布局（不需要改）
title:      bootstrap table 前后端分页案例        # 标题 
subtitle:   前端分页请求至后端案例	# 副标题
date:       2020-05-26              # 时间
author:     Kay                     # 作者
header-img: img/post-bg-2015.jpg    # 这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               # 标签
    - 前端
    - bootstrap
    - java
---

前端代码：  
```
$("#answerLists").bootstrapTable({
    url: '/proxyService/wjtjController/getAnfillblank',
    method: 'POST', //请求方式
    cache: true,
    sidePagination: "server",
    pagination: true, // 分页控件
    pageNumber: 1,
    pageSize: 10,
    pageList: [10, 20, 30, 50],
    locale: "zh-CN",
    queryParams: function (params) {
        //请求参数
        var queryParams = {
            pageNumber: (params.offset / params.limit) + 1,
            pageSize: params.limit,
            sortName: params.sort,
            sortOrder: params.order,
            questionid: questionid,
        }
        return JSON.stringify(queryParams);
    },
    onLoadSuccess: function (response) {
        // 服务器请求加载成功时执行
        var data = response.data;
        //初始化标题
        $("#surveyDescribe").empty();
        $("#surveyDescribe").append(data.question.title != null ? data.question.title : "");

        //初始化表格
        $("#answerLists").bootstrapTable('load', data);
    },
    columns: [
        {
            field : 'index',
            title : "#",
            align : 'center',
            width: "10%",
            formatter : function(value, row, index) {
                var val = index + 1;
                return val;
            }
        },
        {
            title: '答案',
            field: 'answer',
            align: 'center',
            width: "90%"
        }
    ]
});
```

后端代码（java）：  
```
/**
 * 分页查询填空题答案
 * 原理：1、查询用户是否存在该问题，
 * 2、返回该问题答案
 * @param reqMap
 * @return
 */
public String getAnfillblank(Map<String, Object> reqMap) {
    Map<String, Object> model = new HashMap<>();
    String userid = reqMap.get("userId").toString();//用户id
    String questionid = reqMap.get("questionid").toString();//问题id
    int pageNumber = (Integer) reqMap.getOrDefault(PAGE_NUMBER,1);//页数
    int pageSize = (Integer) reqMap.getOrDefault(PAGE_SIZE, 20);//页大小
    Question question = wjtjService.getQuestion (userid, questionid);

    if (question == null){
        //判断用户是否拥有该问题
        return new DataResponse("300", "查询不到该问题！！").toJsonString();
    }

    model.put("question", question);
    PageInfo<AnFillblank> anFillblankList = wjtjService.getAnFillblankList(pageNumber, pageSize, questionid);

    model.put("rows", anFillblankList.getList());//将list放在rows，这是bootstrap硬性要求
    model.put("total", anFillblankList.getTotal());//总条数

    return new DataResponse(model).toJsonString();
}
```
