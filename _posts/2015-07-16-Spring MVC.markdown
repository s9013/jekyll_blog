---
layout: post
title:  "Spring MVC"
categories: Java
---

#MVC
	MVC: 模型(model)、视图(view)、控制器(controller)
	是一种架构模式，程序分层。
	1.模型（model）：业务数据的表示。
	2.视图（view）：视图展现，为用户提供UI，数据的展现。
	3.控制器（controller）：调用业务逻辑产生合适的数据（Model），传递数据给视图层来展现。
	
	Spring MVC的实现
	前端控制器（Front controller） 
	Controller
	View template

#Spring	MVC

	MVC
	Dispatcher
	MVC的核心思想是业务数据抽取同业务数据呈现相分离。
	控制器：负责业务数据的抽取
	视图模板：负责页面呈现
	前端控制器：负责分发调度

	DispacherServlet		前端控制器
	Controller				控制器
	HandlerAdapter			适配器
	HandlerInterceptor		拦截器
	HandlerMapping			前端控制器找到控制器
	HandlerExecutionChain	执行链（反射机制）
	ModelAndView			
	ViewResolver			视图解析器
	View					呈现页面


###Spring MVC welcome-file-list无效
	在Spring MVC配置文件dispatcher-servlet.xml中添加：<mvc:default-servlet-handler/>


###spring mvc 文件上传
	1.导入fileupload架包
	    <dependency>
	        <groupId>commons-fileupload</groupId>
	        <artifactId>commons-fileupload</artifactId>
	        <version>1.3.1</version>
	    </dependency>
	
	2.配置
	    <!-- 上传文件拦截，设置最大上传文件大小 10M=10*1024*1024(B)=10485760 bytes -->
	    <bean id="multipartResolver"
	        class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
	        <property name="maxUploadSize" value="10485760" />
	        <property name="defaultEncoding" value="UTF-8" />
	    </bean> 
	3.编码设置
	    <form action="api/file/upload" method="post" enctype="multipart/form-data">
	        <input type="file" name="files" multiple="multiple"/>
	        <input type="submit" value="submit" />
	    </form>
	4.controller
	    @RequestMapping(value = "upload")
	    private void upload(@RequestParam(value = "files") MultipartFile[] files) throws IllegalStateException, IOException {
	        log.info("upload");
	        for (int i = 0; i < files.length; i++) {
	            MultipartFile file = files[i];
	            file.transferTo(new File("d:/test.txt"));
	        }
	    }

![scorption](https://avatars0.githubusercontent.com/u/8603342?v=3&u=17c90bd9ee618bb5472870d9932994e1e287c08f&s=140)