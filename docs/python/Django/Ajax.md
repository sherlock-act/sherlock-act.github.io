### Ajax

* **基本概念**

异步的javascript。对页面进行局的刷新，ajax请求都在后台。图片，css文件，js文件都是静态文件。

1. 发起ajax请求：jquery发起

2. 执行相应的视图函数，返回json内容

3. 执行相应的回调函数。通过判断json内容，进行相应处理。

![](images/ajax请求流程.png)

```javascript
$(function () {
            $('#btnLogin').click(function () {
                // 1.获取用户名和密码
                username = $('#username').val()
                password = $('#password').val()
                // 2.发起post ajax请求，/login_ajax_check, 携带用户名和密码
                $.ajax({
                    'url':'/login_ajax_check',
                    'type': 'post',
                    'data': {'username':username, 'password':password},
                    'dataType': 'json'
                }).success(function (data) {
                    // 登录成功 {'res':1}
                    // 登录失败 {'res':0}
                    if (data.res == 0){
                        $('#errmsg').show().html('用户名或密码错误')
                    }
                    else{
                        // 跳转到首页
                        location.href = '/index'
                    }
                })
            })
        })
```

---

### 