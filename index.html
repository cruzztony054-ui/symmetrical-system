<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>T-WORLD</title>
<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
<style>
body{background:#101827;color:white;font-family:Arial;padding:20px}
main{max-width:500px;margin:auto}
h1{text-align:center;color:#36d6a5}
.card{background:#1d293b;padding:18px;border-radius:12px;margin:15px 0}
input,button{box-sizing:border-box;width:100%;padding:13px;margin:7px 0;border:0;border-radius:7px;font-size:16px}
input{background:white;color:#111}
button{background:#36d6a5;color:#102018;font-weight:bold}
.secondary{background:#34445c;color:white}
#app{display:none}
#chatbox{height:280px;overflow-y:auto;background:#101827;padding:10px;border-radius:8px}
.message{background:#34445c;padding:10px;margin:7px 0;border-radius:8px;overflow-wrap:anywhere}
.mine{background:#087d62;text-align:right}
</style>
</head>
<body>
<main>
<h1>T-WORLD</h1>
<p style="text-align:center">Connect. Chat. Stay private.</p>

<section id="auth" class="card">
<h3>Login</h3>
<input id="email" type="email" placeholder="Email address">
<input id="password" type="password" placeholder="Password">
<button onclick="login()">Login</button>
<hr>
<h3>Create account</h3>
<input id="fullname" placeholder="Full name">
<input id="username" placeholder="Username">
<input id="newemail" type="email" placeholder="Email address">
<input id="newpassword" type="password" placeholder="Create password">
<button onclick="register()">Create account</button>
<p id="status"></p>
</section>

<section id="app">
<div class="card">
<h3 id="welcome">Welcome</h3>
<button class="secondary" onclick="logout()">Log out</button>
</div>
<div class="card">
<h3>Find people</h3>
<input id="search" placeholder="Search username">
<button onclick="searchUsers()">Search</button>
<div id="results"></div>
</div>
<div class="card">
<h3 id="chatTitle">Private messages</h3>
<div id="chatbox">Choose someone to chat with.</div>
<input id="message" placeholder="Write a message">
<button onclick="sendMessage()">Send message</button>
<p id="chatStatus"></p>
</div>
</section>
</main>

<script>
const URL="https://szlsitwlvlcohcodhazu.supabase.co";
const KEY="sb_publishable_4t9X38e8lhJuwTB3KpaEfg_jfYwLcPS";
const db=window.supabase.createClient(URL,KEY);

let me=null, profile=null, friend=null;

function say(t){document.getElementById("status").textContent=t;}

async function enter(user){
me=user;
let r=await db.from("profiles").select("*").eq("id",user.id).maybeSingle();
if(r.error)throw r.error;
profile=r.data;
if(!profile){
let p=await db.from("profiles").insert({
id:user.id,
full_name:user.user_metadata.full_name||"",
username:user.user_metadata.username||""
}).select().single();
if(p.error)throw p.error;
profile=p.data;
}
document.getElementById("auth").style.display="none";
document.getElementById("app").style.display="block";
document.getElementById("welcome").textContent="Welcome @"+profile.username;
say("");
}

async function register(){
let full_name=document.getElementById("fullname").value.trim();
let username=document.getElementById("username").value.trim().toLowerCase();
let email=document.getElementById("newemail").value.trim();
let password=document.getElementById("newpassword").value;
if(!full_name||!username||!email||!password){say("Fill in all fields.");return;}
if(password.length<6){say("Password must be at least 6 characters.");return;}
say("Creating account...");
let r=await db.auth.signUp({email,password,options:{data:{full_name,username}}});
if(r.error){say(r.error.message);return;}
if(!r.data.session){say("Check your email to confirm your account, then log in.");return;}
try{await enter(r.data.user);}catch(e){say(e.message);}
}

async function login(){
let email=document.getElementById("email").value.trim();
let password=document.getElementById("password").value;
say("Logging in...");
let r=await db.auth.signInWithPassword({email,password});
if(r.error){say(r.error.message);return;}
try{await enter(r.data.user);}catch(e){say(e.message);}
}

async function searchUsers(){
let term=document.getElementById("search").value.trim().toLowerCase();
let box=document.getElementById("results");
if(!term){box.textContent="Enter a username.";return;}
box.textContent="Searching...";
let r=await db.from("profiles").select("id,username,full_name").ilike("username","%"+term+"%").neq("id",me.id).limit(20);
if(r.error){box.textContent=r.error.message;return;}
box.innerHTML="";
if(!r.data.length){box.textContent="No users found.";return;}
r.data.forEach(p=>{
let b=document.createElement("button");
b.className="secondary";
b.textContent=(p.full_name||p.username)+" (@"+p.username+")";
b.onclick=()=>openChat(p);
box.appendChild(b);
});
}

async function openChat(p){
friend=p;
document.getElementById("chatTitle").textContent="Chat with @"+p.username;
await loadMessages();
}

async function loadMessages(){
if(!friend)return;
let box=document.getElementById("chatbox");
box.textContent="Loading...";
let r=await db.from("messages").select("*")
.or("and(sender_id.eq."+me.id+",receiver_id.eq."+friend.id+"),and(sender_id.eq."+friend.id+",receiver_id.eq."+me.id+")")
.order("created_at",{ascending:true});
if(r.error){box.textContent=r.error.message;return;}
box.innerHTML="";
if(!r.data.length){box.textContent="No messages yet. Say hello!";return;}
r.data.forEach(m=>{
let d=document.createElement("div");
d.className="message"+(m.sender_id===me.id?" mine":"");
d.textContent=m.content;
box.appendChild(d);
});
box.scrollTop=box.scrollHeight;
}

async function sendMessage(){
let input=document.getElementById("message");
let content=input.value.trim();
let s=document.getElementById("chatStatus");
if(!friend){s.textContent="Choose someone first.";return;}
if(!content)return;
let r=await db.from("messages").insert({
sender_id:me.id,receiver_id:friend.id,content
});
if(r.error){s.textContent=r.error.message;return;}
input.value="";
s.textContent="";
await loadMessages();
}

async function logout(){
await db.auth.signOut();
me=null;profile=null;friend=null;
document.getElementById("app").style.display="none";
document.getElementById("auth").style.display="block";
say("Logged out.");
}

async function start(){
let r=await db.auth.getSession();
if(r.data.session){
try{await enter(r.data.session.user);}catch(e){say(e.message);}
}
}
start();
</script>
</body>
</html>
