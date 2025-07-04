<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Ashish Mac OS</title>
  <style>
    * {margin: 0; padding: 0; box-sizing: border-box;}
    html, body {height: 100%; font-family: sans-serif; overflow: hidden;}
    #boot, #login, #desktop {
      position: absolute; width: 100%; height: 100%;
    }
    #boot {
      background: black; color: white;
      display: flex; justify-content: center; align-items: center; flex-direction: column;
    }
    #boot img {width: 100px; animation: fade 2s infinite alternate;}
    @keyframes fade { from {opacity: 0.2;} to {opacity: 1;} }
    #login {
      background: linear-gradient(to top right, #333, #666);
      display: none; justify-content: center; align-items: center; flex-direction: column;
      color: white;
    }
    #desktop {
      display: none;
      background-image: url('https://wallpapercave.com/wp/wp2757874.jpg');
      background-size: cover;
    }
    .icon {
      width: 70px; text-align: center; color: white; cursor: pointer; position: absolute;
    }
    .icon img { width: 64px; height: 64px; }
    .window {
      position: absolute; width: 500px; height: 300px;
      background: white; box-shadow: 0 0 10px black; border-radius: 6px; overflow: hidden;
    }
    .window-header {
      background: #444; color: white; padding: 5px;
      display: flex; justify-content: space-between;
    }
    .window-body {padding: 10px; height: 100%; overflow: auto;}
    .dock {
      position: absolute; bottom: 10px; left: 50%; transform: translateX(-50%);
      display: flex; gap: 10px; background: rgba(0,0,0,0.5); padding: 5px 10px; border-radius: 15px;
    }
    .dock img {width: 48px; height: 48px; cursor: pointer;}
  </style>
</head>
<body>

<div id="boot">
  <img src="https://upload.wikimedia.org/wikipedia/commons/f/fa/Apple_logo_black.svg" />
  <p>Booting Ashish Mac OS...</p>
</div>

<div id="login">
  <h2>Welcome, Ashish</h2>
  <input type="password" id="pass" placeholder="Enter password" />
  <button onclick="login()">Login</button>
</div>

<div id="desktop">
  <div class="icon" onclick="openApp('notepad')" style="top:30px;left:30px">
    <img src="https://icons.iconarchive.com/icons/custom-icon-design/mono-general-4/512/notepad-icon.png"><br>Notepad
  </div>

  <div class="dock">
    <img src="https://icons.iconarchive.com/icons/google/chrome/512/Google-Chrome-icon.png" onclick="openApp('browser')">
    <img src="https://icons.iconarchive.com/icons/paomedia/small-n-flat/1024/calculator-icon.png" onclick="openApp('calc')">
    <img src="https://icons.iconarchive.com/icons/microsoft/fluentui-emoji-flat/512/Paintbrush-Flat.png" onclick="openApp('paint')">
    <img src="https://icons.iconarchive.com/icons/dakirby309/windows-8-metro/256/Apps-Windows-Media-Player-Metro-icon.png" onclick="openApp('media')">
    <img src="https://icons.iconarchive.com/icons/papirus-team/papirus-apps/512/terminal-icon.png" onclick="openApp('terminal')">
  </div>
</div>

<script>
setTimeout(() => {
  document.getElementById('boot').style.display = 'none';
  document.getElementById('login').style.display = 'flex';
}, 1500);

function login() {
  if (document.getElementById('pass').value === "1234") {
    document.getElementById('login').style.display = 'none';
    document.getElementById('desktop').style.display = 'block';
  } else {
    alert("Wrong password!");
  }
}

function openApp(app) {
  const win = document.createElement('div');
  win.className = 'window';
  win.style.top = '100px';
  win.style.left = '100px';

  let content = '';
  if (app === 'notepad') {
    content = '<textarea style="width:100%;height:100%;border:none;">Hello, World!</textarea>';
  } else if (app === 'calc') {
    content = '<iframe src="https://www.online-calculator.com/full-screen-calculator/" style="width:100%;height:100%;border:none;"></iframe>';
  } else if (app === 'browser') {
    window.open('https://www.google.com', '_blank'); return;
  } else if (app === 'media') {
    content = '<video src="https://www.w3schools.com/html/mov_bbb.mp4" controls autoplay style="width:100%;height:100%;"></video>';
  } else if (app === 'terminal') {
    content = '<pre>>_ Terminal coming soon</pre>';
  } else if (app === 'paint') {
    content = '<p>Paint app coming soon</p>';
  }

  win.innerHTML = `<div class="window-header">
    <span>${app.toUpperCase()}</span>
    <button onclick="this.closest('.window').remove()">X</button>
  </div>
  <div class="window-body">${content}</div>`;

  document.body.appendChild(win);
}
</script>

</body>
</html>
