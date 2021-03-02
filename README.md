# bilibili-时长进度统计
根据时长统计【B站】当前列表观看进度

* 打开B站列表页面，进入当前学习的章节
![image](https://user-images.githubusercontent.com/19685148/109675277-9b031e00-7bb2-11eb-81b9-725570685b14.png)

* F12打开控制台,拷贝以下代码，根据需要修改targetPageNum后的数值为需要统计的页号,按下回车执行
```javascript
var targetPageNum = 1; //修改为当前观看到的页号，第一个为1。
var menuList = $(jQuery('.list-box .duration'));
if(targetPageNum < 0 || targetPageNum > menuList.length) {
    alert("页号范围为0-" + menuList.length);
}else {
    var currentHour = caculateHour(targetPageNum);
    var totalHour = caculateHour(menuList.length);
    var percent = ((currentHour / totalHour) * 100).toFixed(2) + "%";
    console.log("当前播单观看进度:" + percent + "。观看总时长" + currentHour.toFixed(2) + "小时,播单总时长" + totalHour.toFixed(2) + "小时");
}

function caculateHour(index) {
    let hour = 0.0;
    for(var i = 0; i < index; i++) {
        let hourArr = menuList[i].innerText.split(":");
        
        if(hourArr.length === 4) {
            hour += parseInt(hourArr[0]) * 24.0;
            hour += (parseInt(hourArr[1]) * 1.0);
            hour += (parseInt(hourArr[2]) * 1.0 / 60);
            hour += (parseInt(hourArr[3]) * 1.0 / 3600);
        }

        if(hourArr.length === 3) {
            hour += parseInt(hourArr[0]) * 1.0;
            hour += (parseInt(hourArr[1]) * 1.0 / 60);
            hour += (parseInt(hourArr[2]) * 1.0 / 3600);
        }

        if(hourArr.length === 2) {
            hour += (parseInt(hourArr[0]) * 1.0 / 60);
            hour += (parseInt(hourArr[1]) * 1.0 / 3600);
        }

        if(hourArr.length === 1) {
            hour += (parseInt(hourArr[0]) * 1.0 / 3600);
        }
    }

    return hour;
}
```
![image](https://user-images.githubusercontent.com/19685148/109676764-fd105300-7bb3-11eb-8f7c-d9a71655e6bc.png)

* 如下
![image](https://user-images.githubusercontent.com/19685148/109676936-20d39900-7bb4-11eb-8847-7001459a4f78.png)
