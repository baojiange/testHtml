# testHtml
html数据转换测试



<!DOCTYPE html>
<html lang="ch">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<script>
    var json = [
        {'day1':'上午','username':'张三','id':'001','day2':'星期一'},
        {'day1':'上午','username':'aaa','id':'003','day2':'星期二'},
        {'day1':'下午','username':'bbb','id':'004','day2':'星期二'},
        {'day1':'下午','username':'ddd','id':'006','day2':'星期三'},
        {'day1':'下午','username':'fff','id':'008','day2':'星期四'},
        {'day1':'上午','username':'eee','id':'007','day2':'星期三'},
        {'day1':'上午','username':'ggg','id':'009','day2':'星期四'},
        {'day1':'下午','username':'hhh','id':'010','day2':'星期五'},
         {'day1':'下午','username':'浮动幅度','id':'002','day2':'星期一'},
        {'day1':'上午','username':'ttt','id':'011','day2':'星期五'},
        {'day1':'下午','username':'rrr','id':'012','day2':'星期六'},
        {'day1':'下午','username':'bbb','id':'014','day2':'星期日'},
        {'day1':'上午','username':'vvv','id':'015','day2':'星期日'},
        {'day1':'上午','username':'qqq','id':'013','day2':'星期六'}
    ];
    document.write("初始化json数据..............<br/><br/>");
    document.write(JSON.stringify(json)+"<br/><br/>");
    document.write("处理json数据..............<br/><br/>");
    var arr1 = [];
      var map1 = {};//上午
      map1.arrs = [];
      var map2 = {};//下午
      map2.arrs = [];
    for(var i=0;i<json.length;i++){
        if(json[i].day1=="上午"){
           map1.key=json[i].day1;
           map1.arrs.push(json[i]);
        }else if(json[i].day1=="下午"){
           map2.key=json[i].day1;
           map2.arrs.push(json[i]);
        }
    }
    arr1.push(map1);
    arr1.push(map2);
    document.write(JSON.stringify(arr1)+"<br/><br/>");

    var weeks = ['星期一','星期二','星期三','星期四','星期五','星期六','星期日'];
    var result = [];
    for(var k=0;k<arr1.length;k++){
      var objs = {};
      objs.key=arr1[k].key;
      objs.value='';
      var weekData = [];
      for(var i=0;i<weeks.length;i++){
        var weekObj = {};
          var amArrs = arr1[k].arrs;
                for(var j=0;j<amArrs.length;j++){
                    if(weeks[i]==amArrs[j].day2){
                        weekObj.day2=weeks[i];
                        weekObj.day1 = amArrs[j].day1;
                        weekObj.username = amArrs[j].username;
                        weekObj.id = amArrs[j].id;
                        weekData.push(weekObj);
                        break;
                        }
                }
                console.log(weekObj);
             if(JSON.stringify(weekObj)=='{}'){
                console.log("111");
                        weekObj.day2=weeks[i];
                        weekObj.day1 = arr1[k].key;
                        weekObj.username = '';
                        weekObj.id = '';
                weekData.push(weekObj);
             }

        }
        objs.value=weekData;
        result.push(objs);
    }
    console.log(JSON.stringify(result));
    var html = "<table><head></table>";
    document.write("<table><thead>");
    document.write("<th></th>");
    for(var i=0;i<weeks.length;i++){
        document.write("<th>"+weeks[i]+"</th>");
    }
     document.write("</thead>");
    document.write("<tbody>");
    for(var i=0;i<result.length;i++){
        document.write("<tr>");
        document.write("<td>"+result[i].key+"</td>");
        for(var j=0;j<result[i].value.length;j++){
            var objStr = JSON.stringify(result[i].value[j]);
            document.write("<td>"+objStr+"</td>");
        }
        document.write("</tr>");
    }
    document.write("</tbody>");
    document.write("</table>");
</script>
<body>
    <table><thead><th></th></thead></table>
</body>
</html>
