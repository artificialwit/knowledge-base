# Single Page app

### Url Rewrite and HtAcess 

```html
//index.html
<!DOCTYPE html>
<html>
  <head>
    <title>My app</title>
    <meta charset="UTF-8" />
    <link rel="stylesheet" href="./src/styles.css" />
  </head>
  <body>
    <h1>My App</h1>
    <nav>
      <ul class="menu">
        <li class="menu_item" value="home">Home</li>
        <li class="menu_item" value="about">About</li>
        <li class="menu_item" value="pricing">Pricing</li>
      </ul>
    </nav>
    <main>
      <section id="container"></section>
    </main>
    <footer>2022@Artifial</footer>
    <script src="index.js"></script>
  </body>
</html>

```

```txt
// .htaccess

RewriteEngine on
RewriteRule ^([a-zA-Z0-9]+)$ index.html?path=$1

```


```index.js
window.onload = function () {
  const path = window.location.pathname.split("/");
  switch (path[1]) {
    case "": {
      loadPage("home");
      break;
    }
    case "about": {
      loadPage("about");
      break;
    }
    case "pricing": {
      loadPage("pricing");
      break;
    }
    default: {
      loadPage("404");
      break;
    }
  }

  document.querySelectorAll(".menu_item").forEach((item) => {
    item.addEventListener("click", function () {
      const path = item.getAttribute("value");
      loadPage(path);
      if (path === "home") {
        window.history.pushState("", "", "/");
        return;
      }
      window.history.pushState("", "", path);
    });
  });

  function loadPage(path) {
    console.log("load funciton : ", path);
    if (path === "") return;

    const container = document.getElementById("container");

    const request = new XMLHttpRequest();
    request.open("GET", "/pages/" + path + ".html");
    request.send();
    request.onload = function () {
      if (request.status === 200) {
        document.title= path;
        container.innerHTML = request.responseText;
      }
    };
  }
};


```
