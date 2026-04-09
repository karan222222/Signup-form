# Signup-form
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Secure Login & Signup</title>

<style>
:root{
  --primary:#0d6efd;
  --dark:#0b1220;
  --glass:rgba(255,255,255,0.12);
  --border:rgba(255,255,255,0.25);
}

*{
  margin:0;
  padding:0;
  box-sizing:border-box;
  font-family: "Segoe UI", system-ui, sans-serif;
}

body{
  min-height:100vh;
  display:flex;
  align-items:center;
  justify-content:center;
  background:linear-gradient(135deg,#0d6efd,#0b1220);
}

/* ================= CARD ================= */
.container{
  width:380px;
  max-width:95%;
  background:var(--glass);
  backdrop-filter:blur(18px);
  border-radius:22px;
  padding:30px;
  color:#fff;
  box-shadow:0 25px 60px rgba(0,0,0,.45);
  animation:fadeIn .8s ease;
}

@keyframes fadeIn{
  from{opacity:0; transform:translateY(25px);}
  to{opacity:1; transform:translateY(0);}
}

h2{
  text-align:center;
  margin-bottom:22px;
  font-weight:600;
}

/* ================= INPUT ================= */
.input-box{
  position:relative;
  margin-bottom:18px;
}

.input-box input{
  width:100%;
  padding:13px 45px 13px 15px;
  border-radius:30px;
  border:2px solid transparent;
  outline:none;
  background:rgba(255,255,255,.15);
  color:#fff;
  font-size:15px;
  transition:.3s;
}

.input-box input::placeholder{
  color:#ddd;
}

.input-box input:focus{
  border-color:var(--primary);
  background:rgba(255,255,255,.18);
}

.toggle-pass{
  position:absolute;
  right:15px;
  top:50%;
  transform:translateY(-50%);
  cursor:pointer;
  opacity:.7;
}

/* ================= BUTTON ================= */
button{
  width:100%;
  padding:13px;
  border-radius:30px;
  border:2px solid var(--primary);
  background:transparent;
  color:#fff;
  font-size:16px;
  cursor:pointer;
  transition:.35s;
  margin-top:8px;
}

button:hover{
  background:var(--primary);
  transform:scale(1.05);
}

button:active{
  transform:scale(.98);
}

/* ================= LINKS ================= */
.forgot{
  text-align:right;
  font-size:14px;
  color:#aad4ff;
  cursor:pointer;
  margin-bottom:10px;
}

.switch{
  text-align:center;
  margin-top:16px;
  cursor:pointer;
  color:#aad4ff;
}

/* ================= LOADER ================= */
.loader{
  display:none;
  text-align:center;
  margin-top:10px;
}

/* ================= MODAL ================= */
.modal{
  position:fixed;
  inset:0;
  background:rgba(0,0,0,.65);
  display:none;
  align-items:center;
  justify-content:center;
}

.modal-content{
  background:var(--dark);
  padding:25px;
  border-radius:16px;
  width:320px;
  color:#fff;
  animation:scaleIn .3s ease;
}

@keyframes scaleIn{
  from{transform:scale(.85); opacity:0;}
  to{transform:scale(1); opacity:1;}
}

/* ================= RESPONSIVE ================= */
@media(max-width:480px){
  .container{
    padding:22px;
  }
}
</style>
</head>

<body>

<div class="container">
  <h2 id="title">Login</h2>

  <div class="input-box" id="nameBox" style="display:none">
    <input type="text" id="name" placeholder="Full Name">
  </div>

  <div class="input-box">
    <input type="email" id="email" placeholder="Email address">
  </div>

  <div class="input-box">
    <input type="password" id="password" placeholder="Password">
    <span class="toggle-pass" onclick="togglePass()">👁</span>
  </div>

  <div class="forgot" onclick="openModal()">Forgot Password?</div>

  <button onclick="submitForm()">Continue</button>

  <div class="loader" id="loader">⏳ Please wait...</div>

  <div class="switch" onclick="toggleForm()">
    Don’t have an account? Sign Up
  </div>
</div>

<!-- ================= MODAL ================= -->
<div class="modal" id="modal">
  <div class="modal-content">
    <h3>Reset Password</h3><br>
    <input type="email" id="resetEmail" placeholder="Enter email"
      style="width:100%;padding:10px;border-radius:20px;border:none"><br><br>
    <button onclick="closeModal()">Send Reset Link</button>
  </div>
</div>

<script>
let isLogin=true;

function toggleForm(){
  isLogin=!isLogin;
  document.getElementById("title").innerText=isLogin?"Login":"Create Account";
  document.getElementById("nameBox").style.display=isLogin?"none":"block";
  document.querySelector(".switch").innerText=
    isLogin?"Don’t have an account? Sign Up":"Already have an account? Login";
}

function togglePass(){
  const pass=document.getElementById("password");
  pass.type = pass.type==="password" ? "text" : "password";
}

function submitForm(){
  const email=document.getElementById("email").value.trim();
  const pass=document.getElementById("password").value.trim();
  const name=document.getElementById("name").value.trim();

  if(!email || !pass || (!isLogin && !name)){
    alert("Please fill all required fields");
    return;
  }

  document.getElementById("loader").style.display="block";

  setTimeout(()=>{
    document.getElementById("loader").style.display="none";
    alert(isLogin?"Login successful 🎉":"Account created successfully 🎉");
  },1200);
}

function openModal(){
  document.getElementById("modal").style.display="flex";
}

function closeModal(){
  document.getElementById("modal").style.display="none";
}
</script>

</body>
</html>
