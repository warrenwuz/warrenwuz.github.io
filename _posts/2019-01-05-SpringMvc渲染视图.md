---
layout:     post
title:      SpringMvc渲染视图
subtitle:   Spring实战学习笔记 SpringMvc渲染视图
date:       2019-01-05
author:     warren
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - Spring
    - Java
    - Spring Mvc
---

## 视图解析

视图解析器|描述
---|---
FreeMarkViewResolver | 将视图解析为FreeMarker模板
InternalResourceViewResolver | 将视图解析为Web应用的内部资源(*.jsp)
VelocityViewResolver|将视图解析为Velocity布局,Velocity模板
### InternalResourceViewResolver
```
@Bean
	public ViewResolver viewResolver(){
		InternalResourceViewResolver resourceViewResolver=new InternalResourceViewResolver();
		resourceViewResolver.setPrefix("/WEB-INF/views/");
		resourceViewResolver.setSuffix(".jsp");
		//加入Spring标签支持
		resourceViewResolver.setViewClass(org.springframework.web.servlet.view.JstlView.class);
		resourceViewResolver.setExposeContextBeansAsAttributes(true);
		return resourceViewResolver;
	}

```

#### SpringForm标签库
```
<%@ taglib uri="http://www.springframework.org/tags/form" prefix="sf" %>
<!--commandName 已经被Spring去掉了 新特性是modelAttribute-->
<sf:form method="post" modelAttribute="spitter">
	Fist Name: <sf:input path="firstName"></sf:input> <br/>
	<span  id="firstNameError">	<sf:errors path="firstName"/></span>
	Last Name: <sf:input path="lastName"></sf:input> <br/>
	email: <sf:input path="email"></sf:input> <br/>
	username: <sf:input path="username"></sf:input> <br/>
	password: <sf:input path="password"></sf:input> <br/>
	<input type="submit" value="Register">
</sf:form
```
#### Spring通用标签库

```
<%@ taglib uri="http://www.springframework.org/tags" prefix="s" %>
<!--可以让url携带参数 javaScriptEscape属性为true可以在js中使用-->
<s:url href="/spittles/{username}" var="spittlesUrl" javaScriptEscape="true">
<s:param name="max" value="60">
<s:param name="count" value="20">
<s:param name="username" value="wz">
</s:url>
<!--转义html-->
<s:escapeBody javaScriptEscape="true"><h1>Hello</h1></s:escapeBody>
```

JSP标签| 描述
---|---
<s:escapeBody> | 将标签中的内容进行HTML或JavaScript转义
<s:eval> | 计算符合Spring表达式语言（SpEl）


