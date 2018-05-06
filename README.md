# binbin07
<!DOCTYPE html>
<html>
<head>
	<title>binbin 06</title>
<style type="text/css">
	ul li{
		height: 30px;
		list-style-type: none;
		background-color: red;
		border: 1px solid #999;
		float: left;
		color: white;
		margin: 5px;
		text-align: center;
		padding: 0px 10px;
	}
	.yellow{
		height: 30px;
		list-style-type: none;
		background-color:#FFFF00;
		border: 1px solid #999;
		float: left;
		color: white;
		margin: 5px;
		text-align: center;
		padding: 0px 10px;
	}
</style>
</head>
<body>
<textarea id="text" onfocus="myFunction(this)"></textarea>
<button id="left-in">左侧入</button>
<button id="left-out">左侧出</button>
<button id="right-in">右侧入</button>
<button id="right-out">右侧出</button>
<ul id="line">
	<li >10</li>
	<li >3</li>
	<li >7</li>
	<li >12</li>
	<li >11</li>
	<li >30</li>
</ul>
<p style="clear: both;">
<input type="text" id="text1" onfocus="myFunction(this)">
<button id="search">查询</button>
</p>
<script type="text/javascript">
	var a = document.getElementById("left-in");
	var b = document.getElementById("left-out");
	var c = document.getElementById("right-in");
	var d = document.getElementById("right-out");
	var e = document.getElementById("text");
	var f = document.getElementById("line");
	var ta = f.getElementsByTagName("li");
	var data = new Array;
	var data0 = new Array;
	for (var i = 0; i < ta.length; i++) {
		data[i] = ta[i].innerHTML;
	}
	function myFunction(x){
		x.value="";
	}
  // 可以通过数组方式，但是每次显示相当于重新加载整个列表。
	function render(data) {
		f.innerHTML = "";
		for (var i = 0; i < data.length; i++) {
			var li = document.createElement("li");
			f.appendChild(li);
			li.innerHTML = data[i];
		}
	}
	function found(value){
		var arr = new Array;
		var a = 0;
		value = value.replace(/[;、.。；，\s\r\n,]/g,",");
		while (value.indexOf(",",a) !=-1){
			a = value.indexOf(",",a);
			arr.push(a);
			a = a + 1;
		}
		data0[0] = value.substring(0,arr[0]);
		data0[0] = data0[0].replace(",","");
		if (arr.length!=0) {
			for (var i = 1; i <= arr.length; i++) {
				data0[i]=value.substring(arr[i-1],arr[i]);
				data0[i]=data0[i].replace(",","");
			}
		} 
		return data0;
	}
	c.onclick = function(){
		found(e.value);
		data = data.concat(data0);
		render(data);
	};
	a.onclick = function(){
		found(e.value);
		data = data0.concat(data);
		render(data);
	};
	b.onclick = function(){
		var item =data.shift();
		render(data);
		alert(item);
	};
	d.onclick = function(){
		var item =data.pop();
		render(data);
		alert(item);
	};
	document.getElementById("search").onclick = function(){
		render(data);
		var sum =0;
		for (var i = 0; i < data.length; i++) {
			if (data[i].indexOf(text1.value)!=-1) {
				f.children[i].className="yellow";
				sum = sum + 1;
			}
		}
		if (sum ==0) {
			alert("大傻蛋！这个数字不存在了啦!");
		}
	};
</script>
</body>
</html>
