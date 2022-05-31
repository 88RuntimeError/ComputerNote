# 一、页面加载函数

```javascript
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<script type="text/javascript" src="js/jquery.min.js" ></script>
		<script>
			/*jQuery(document).ready(function (){
				var domS1=document.getElementById("s1");
				console.log(domS1.innerText);
			})*/
			
			// jQuery  可以简写 $
			/*$(document).ready(function (){
				var domS1=document.getElementById("s1");
				console.log(domS1.innerText);
			})*/
			
			
			$(function(){
				var domS1=document.getElementById("s1");
				console.log(domS1.innerText);
			})
			
			$(function(){
				console.log("第二个页面加载函数")
			})
			
			$(function(){
				console.log("第三个页面加载函数")
			})
			
			
		</script>
	</head>
	<body>
		<span id="s1">测试文字</span>
	</body>
</html>
```



# 二、基本选择器

```javascript
<!DOCTYPE html> 
<html> 
    <head> 
        <meta charset="utf-8"> 
        <title>基本选择器</title> 
         <style type="text/css"> 
            .myClass{ 
                background-color:  aqua; 
            } 
        </style> 
        <script type="text/javascript" src="js/jquery.min.js"></script> 
        <script type="text/javascript"> 
        	// 必须自己会使用的选择器  id选择器  $("#id") 类选择器 $('.class属性值')  标签选择器 $("标签名")
        	
            $(function(){ 
                //标签选择器 $("a")   
                //$("h3").addClass("myClass"); 
                //$("p").addClass("myClass"); 
                //ID选择器 $("#id")     $("p#id") 
                //$("#h31").addClass("myClass"); 
                //$("h3#h31").addClass("myClass"); 
                //类选择器 $(".class")    $("h2.class") 
                //$(".red1").addClass("myClass"); 
                //通配选择器 $("*") 
                //$("*").addClass("myClass"); 
                //并集选择器$("elem1,elem2,elem3") 
                //$("#h31,span,div").addClass("myClass"); 
                //后代选择器$(ul li)   
                //$("p span").addClass("myClass");   
                //父子选择器 $(ul>li)   
                //$("p>span").addClass("myClass"); 
                //后面第一个兄弟元素 prev + next 
                //$("h3+p").addClass("myClass"); 
                //后面所有的兄弟元素 prev ~ next 
                $("h3~p").addClass("myClass"); 
            });               
        </script> 
    </head> 
    <body> 
       <h3 id="h31">JSP</h3> 
       <p>  
	       JSP全名为Java Server Pages，中文名叫java服务器页面，
		       其根本是一个简化的<span>Servlet</span>设计， 它[1]  是
		       由Sun Microsystems公司倡导、许多公司参与一起建立的一种
		       动态网页技术标准。JSP技术有点类似ASP技术，它是在传统的网
		       页<em><span>HTML</span></em>（标准通用标记语言的子集）
		       文件(*.htm,*.html)   中插入Java程序段(Scriptlet)和JSP
		       标记(tag)，从而形成JSP文件，后缀名为(*.jsp)。 用JSP开发
		       的Web应用是跨平台的，既能在Linux下运行，也能在其他操作系
		       统上运行。 
       </p>  
       
       <h3 id="h32"   class="red1">Servlet</h3> 
       
       <p> 
       	    Servlet（Server Applet）是Java Servlet的简称，是为小服
       	    务程序或服务连接器，用Java编写的服务器端程序，主要功能在于
       	    交互式地浏览和修改数据，生成动态Web内容。 
       </p> 
       
       <p class="red1"> 
          	狭义的Servlet是指Java语言实现的一个接口，广义的Servlet
          	是指任何实现了这个Servlet接口的类，一般情况下，人们将
          	Servlet理解为后者。Servlet运行于支持Java的应用服务器中。
          	从原理上讲，Servlet可以响应任何类型的请求，但绝大多数情
          	况下Servlet只用来扩展基于HTTP协议的Web服务器。 
       </p> 
       
      <div> 
        <p>div   p</p>   
      </div> 
      
      <span>span</span> 
      
       <p class="red1"> 
       		狭义的Servlet是指Java语言实现的一个接口，广义的Servlet
       		是指任何实现了这个Servlet接口的类，一般情况下，人们将Servlet
       		理解为后者。Servlet运行于支持Java的应用服务器中。从原理上讲，
       		Servlet可以响应任何类型的请求，但绝大多数情况下Servlet只用
       		来扩展基于HTTP协议的Web服务器。 
       </p>
       
    </body> 
</html>
```



# 三、属性选择器

```javascript
<!DOCTYPE html>
<html>
    <head>
         <meta charset="utf-8">
         <title>属性选择器</title>
         <style type="text/css">
             .myClass {
                  background-color: aqua;
             }
         </style>
         <script src="js/jquery.js"   type="text/javascript"   charset="utf-8"></script>
         <script type="text/javascript">
             $(function() {
                  //[attribute] 
                  //$("a").addClass("myClass"); 
                  //$("a[href]").addClass("myClass"); 
                  //[attribute1][attribute2] 
                  //$("a[href][title]").addClass("myClass"); 
                  //[attribute=value]   
                  //$("a[href='film-2.html']").addClass("myClass"); 
                  //[attribute!=value]   
                  //$("a[href][href!='film-2.html']").addClass("myClass"); 
                  //[attribute^=value]   
                  //$("a[href^='http']").addClass("myClass"); 
                  //[attribute$=value   
                  //$("a[href$='htm']").addClass("myClass"); 
                  //[attribute*=value]   
                  $("a[href*='mashibing']").addClass("myClass");
             });
         </script>
    </head>
    <body>
         <ul id="msb">
             <li>
                  <a href="http://www.mashibing.com/job.html">青花瓷</a>
             </li>
             <li>
                  <a href="http://www.mashibing.com/dorm">小朋友,你是否有很多问号</a>
             </li>
             <li>
                  <a href="http://www.mashibing.com/mobile">羞答答的玫瑰静悄悄的开</a>
             </li>
             <li>
                  <a href="http://www.mashibing.com/flag">月半小夜曲</a>
             </li>
             <li>
                  <a href="http://www.msb.com/film">单恋一枝花</a>
                  <ul id="film">
                      <li>
                          <a href="film-1.html">乱世佳人</a>
                      </li>
                      <li>
                          <a href="film-2.html"   title="阿郎的故事">阿郎的故事</a>
                      </li>
                      <li id="film3">
                          <a href="film-3.html">阿甘正传</a>
                      </li>
                      <li>
                          <a href="http://www.mashibing.com/film/film-4.htm"   title="鲁冰花">鲁冰花</a>
                      </li>
                      <li>
                          <a name="film-5.htm"   title="太行山上">太行山上</a>
                      </li>
                      <li>无问西东</li>
                  </ul>
             </li>
         </ul>
    </body>
</html>
```



# 四、位置选择器

