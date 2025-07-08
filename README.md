<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>키다리여행사</title>
  <style>
    body { font-family: sans-serif; margin: 0; text-align: center; background: #f9f9f9; }
    header { background: #2d9cdb; color: #ffffff; padding: 10px; font-size: 3.0em; }
    iframe { margin: 0px auto; display: block; width: 700px; height: 400px; border: 0; position:absolute;left:30px;top:60px;}
    span { width: 100px; height: 10px; }

    .color { background: #2d9cdb; color: #fff; padding: 10px; font-size: 1.0em;}
    .menu-item:hover {
      color: red;
    }
    .login-box {
      background: #fff; width: 300px; margin: 70px auto; padding: 20px;
      box-shadow: 0 0 10px rgba(0,0,0,.1); border-radius: 8px;
    }
    .login-box input { width: 100%; padding: 0px; margin: 8px 0; box-sizing: border-box; }
    .login-box button {
      width: 100%; padding: 10px; background: #27ae60; color: #fff;
      border: 0; border-radius: 5px; font-weight: bold; cursor: pointer;
    }
    .error { color: red; font-size: .9em; }
    .signup-link {
      display: inline-block; margin-top: 15px; padding: 10px 20px;
      background: #2980b9; color: #fff; text-decoration: none;
      border-radius: 5px; font-weight: bold;
    }
  </style>
</head>
<body>

<header>키다리여행사</header>

<div class="color">
  <span class="menu-item" id="area1">유럽</span> |
  <span class="menu-item" id="area2">아시아</span> |
  <span class="menu-item" id="area3">아프리카</span> |
  <span class="menu-item" id="area4">오세아니아</span> |
  <span class="menu-item" id="area5">북미</span> |
  <span class="menu-item" id="area6">남미</span>
</div>


<div id=if style="position:absolute;left:180px;top:70px;">
<iframe
  src="https://www.youtube.com/embed/pN1Z1qllu7k?autoplay=1&mute=1&loop=1&playlist=pN1Z1qllu7k"
  allow="autoplay; encrypted-media" allowfullscreen>
</iframe>
</div>

<div class="login-box" style="position:absolute;left:920px;top:60px;">
  <h3>로그인</h3>
  <input type="text" id="loginId" placeholder="아이디">
  <input type="password" id="loginPw" placeholder="비밀번호">
  <button onclick="login()">로그인</button>
  <div id="loginError" class="error"></div>

  <a class="signup-link" href="signup1.html">회원가입</a>
</div>

<!-- <script>
    document.getElementById('area1').addEventListener('mouseover', () => {
    area1.style.color = 'red';
    });
    document.getElementById('area1').addEventListener('mouseout', () => {
    area1.style.color = '';
    });
</script> -->


<script>
  (function () {
    const users = JSON.parse(localStorage.getItem('users') || '{}');
    if (!users.admin) {
      users.admin = {
        userid: 'admin',
        password: 'passwd',
        name: '관리자',
        phone: '010-0000-0000',
        email: 'admin@kidaritravel.com',
        address: '',
        gender: ''
      };
      localStorage.setItem('users', JSON.stringify(users));
    }
  })();

  function login() {
    const id = document.getElementById('loginId').value.trim();
    const pw = document.getElementById('loginPw').value.trim();
    const users = JSON.parse(localStorage.getItem('users') || '{}');
    const user = users[id];
    const errorBox = document.getElementById('loginError');
    errorBox.textContent = '';

    if (!id || !pw) {
      errorBox.textContent = '아이디와 비밀번호를 모두 입력하세요.';
    } else if (user && user.password === pw) {
      localStorage.setItem('currentUser', id);
      location.href = 'detail1.html';
    } else {
      errorBox.textContent = '아이디 또는 비밀번호가 올바르지 않습니다.';
    }
  }
</script>


</body>
</html>



<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>키다리여행사 회원가입</title>
  <style>
    body { font-family: sans-serif; background: #f9f9f9; margin: 0; }
    h1 { text-align: center; padding: 20px; }
    form {
      width: 400px; margin: 0 auto; background: #fff; padding: 20px;
      box-shadow: 0 0 10px rgba(0,0,0,.1);
    }
    label { display: block; margin-top: 15px; font-weight: bold; }
    input, select {
      width: 100%; padding: 8px; margin-top: 5px; box-sizing: border-box;
    }
    button {
      margin-top: 20px; padding: 10px; width: 100%;
      background: #2d9cdb; color: #fff; border: 0;
      border-radius: 5px; font-size: 1em; cursor: pointer;
    }
    .error { color: red; font-size: .9em; }
  </style>
</head>
<body>

<h1>회원가입</h1>

<form onsubmit="return handleSubmit(event);">
  <label for="userid">아이디 *</label>
  <input type="text" id="userid">
  <div id="useridError" class="error"></div>

  <label for="password">비밀번호 *</label>
  <input type="password" id="password">
  <div id="passwordError" class="error"></div>

  <label for="name">이름 *</label>
  <input type="text" id="name">
  <div id="nameError" class="error"></div>

  <label for="phone">전화번호 *</label>
  <input type="tel" id="phone" placeholder="010-1234-5678">
  <div id="phoneError" class="error"></div>

  <label for="email">이메일 *</label>
  <input type="email" id="email">
  <div id="emailError" class="error"></div>

  <label for="address">주소 (선택)</label>
  <input type="text" id="address">

  <label for="gender">성별 (선택)</label>
  <select id="gender">
    <option value="">선택안함</option>
    <option value="남성">남성</option>
    <option value="여성">여성</option>
  </select>

  <button type="submit">가입하기</button>
</form>

<script>
  function clearErrors() {
    document.querySelectorAll('.error').forEach(el => el.textContent = '');
  }

  function handleSubmit(e) {
    e.preventDefault();
    clearErrors();

    const uid = document.getElementById('userid').value.trim();
    const pw = document.getElementById('password').value.trim();
    const nm = document.getElementById('name').value.trim();
    const ph = document.getElementById('phone').value.trim();
    const em = document.getElementById('email').value.trim();
    const addr = document.getElementById('address').value.trim();
    const gen = document.getElementById('gender').value;

    let ok = true;

    if (!uid) {
      document.getElementById('useridError').textContent = '아이디를 입력하세요.';
      ok = false;
    } else {
      const users = JSON.parse(localStorage.getItem('users') || '{}');
      if (users[uid]) {
        document.getElementById('useridError').textContent = '이미 존재하는 아이디입니다.';
        ok = false;
      }
    }

    if (!pw) {
      document.getElementById('passwordError').textContent = '비밀번호를 입력하세요.';
      ok = false;
    } else if (pw.length < 6) {
      document.getElementById('passwordError').textContent = '6자 이상 입력하세요.';
      ok = false;
    }

    if (!nm) {
      document.getElementById('nameError').textContent = '이름을 입력하세요.';
      ok = false;
    }

    const phoneRx = /^010-\d{4}-\d{4}$/;
    if (!phoneRx.test(ph)) {
      document.getElementById('phoneError').textContent = '예: 010-1234-5678';
      ok = false;
    }

    if (!em) {
      document.getElementById('emailError').textContent = '이메일을 입력하세요.';
      ok = false;
    } else if (!em.includes('@')) {
      document.getElementById('emailError').textContent = '올바른 이메일 형식';
      ok = false;
    }

    if (!ok) return false;

    const users = JSON.parse(localStorage.getItem('users') || '{}');
    users[uid] = {
      userid: uid,
      password: pw,
      name: nm,
      phone: ph,
      email: em,
      address: addr,
      gender: gen
    };
    localStorage.setItem('users', JSON.stringify(users));
    localStorage.setItem('currentUser', uid);

    location.href = 'detail1.html';
    return false;
  }
</script>

</body>
</html>




<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>회원 상세정보</title>
  <style>
    body { font-family: sans-serif; background: #f9f9f9; margin: 0; text-align: center; }
    h1 { background: #2d9cdb; color: #fff; margin: 0; padding: 20px; }
    table {
      margin: 40px auto; border-collapse: collapse; width: 60%; max-width: 500px; background: #fff;
      box-shadow: 0 0 10px rgba(0,0,0,.1);
    }
    th, td { padding: 12px; border-bottom: 1px solid #ddd; text-align: left; }
    th { background: #ecf0f1; width: 120px; }
    a.btn {
      display: inline-block; margin: 20px; padding: 10px 20px; background: #2980b9;
      color: #fff; text-decoration: none; border-radius: 5px; font-weight: bold;
    }
  </style>
</head>
<body>

<h1>회원 상세정보</h1>

<table id="infoTable"></table>

<a href="index1.html" class="btn">메인으로</a>

<script>
  const uid = localStorage.getItem('currentUser');
  const users = JSON.parse(localStorage.getItem('users') || '{}');
  const user = users[uid];

  const table = document.getElementById('infoTable');

  if (!user) {
    table.innerHTML = '<tr><td colspan="2">회원 정보가 존재하지 않습니다.</td></tr>';
  } else {
    const rows = [
      ['아이디', user.userid],
      ['이름', user.name],
      ['전화번호', user.phone],
      ['이메일', user.email],
      ['주소', user.address || '-'],
      ['성별', user.gender || '-']
    ];
    table.innerHTML = rows.map(([k, v]) => `<tr><th>${k}</th><td>${v}</td></tr>`).join('');
  }
</script>

</body>
</html>
