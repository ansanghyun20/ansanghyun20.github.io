
### Spring 에서 Node JS에 UserId Post 요청 해서 html에 출력하는 것


- spring boot 에서 nodeJS 로 Post 요청 하기

```javascript
var params = {}
params['userName'] = document.getElementById("userName").value; // 값을 추가하는 부분
var form = document.createElement('form');
form.setAttribute('method','post');
form.setAttribute('action',roomCode);
document.charset="utf-8";
for ( var key in params) {	// key, value로 이루어진 객체 params
        var hiddenField = document.createElement('input');
        hiddenField.setAttribute('type', 'hidden'); //값 입력
        hiddenField.setAttribute('name', key);
        hiddenField.setAttribute('value', params[key]);
        form.appendChild(hiddenField);
}
document.body.appendChild(form);
form.submit();
            
```

### Post 수령 및 render로 html 값 전송

```nodejs

app.post( '/', ( req, res ) => {
    var userName = req.body.userName;     // post 요청 받은 데이터 담기
    console.log(userName);
    res.render(__dirname+'/index.html',{'userId': userName} );  // 값을 이런식으로 전송한다
} );

```

### html 에서 전송 받은 값 출력하기

```html
<form action = "/" method="post">
  
<span id="hello"> <%= userId %> </span>            <!-- <%= userId %> 이와같이 출력할 수 있다 -->
<script>
  var id = document.getElementById('hello');
  document.write(id.innerText);
  document.getElementById('username').value = id.innerText;
</script>

</form>
  
```
