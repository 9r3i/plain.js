# plain.js
plain text theme for website and blog


# usage
how to use it?

we have to make an html file and one json config.

config file must contain database section, performTest and theme section.

and here is the example of ```hunter.json``` config file:
```json
{
  "version": 231125.1017,
  "name": "hunter.json",
  "database": {
    "driver": "BlogDatabaseDriver",
    "host": "https://api.github.com/repos",
    "username": "9r3i",
    "password": "___PUBLIC_TOKEN___",
    "name": "gaino-blog-data",
    "tables": {
      "posts": "releases",
      "authors": "releases/download/1.0.0/authors.json"
    },
    "file": null,
    "fetch": "browser",
    "expires": "Fri, Nov 23 2024"
  },
  "theme": {
    "host": "https://raw.githubusercontent.com/9r3i/plain.js",
    "namespace": "plain",
    "templates": {
      "footer": "templates/footer.min.js",
      "login": "templates/login.html",
      "main": "templates/main.html"
    },
    "files": [
      "plain.min.css",
      "plain.min.js"
    ],
    "save": true,
    "show_assets": true,
    "mainTagName": "1.0.0",
    "reader": "https://relfo.vercel.app/9r3i/plain.js/reader/",
    "url": "https://raw.githubusercontent.com/9r3i/plain.js"
  },
  "performTest": false,
  "loader": "data:image/gif;base64,R0lGODlhEAALAPQAAP///wAAANra2tDQ0Orq6gYGBgAAAC4uLoKCgmBgYLq6uiIiIkpKSoqKimRkZL6+viYmJgQEBE5OTubm5tjY2PT09Dg4ONzc3PLy8ra2tqCgoMrKyu7u7gAAAAAAAAAAACH5BAkLAAAAIf4aQ3JlYXRlZCB3aXRoIGFqYXhsb2FkLmluZm8AIf8LTkVUU0NBUEUyLjADAQAAACwAAAAAEAALAAAFLSAgjmRpnqSgCuLKAq5AEIM4zDVw03ve27ifDgfkEYe04kDIDC5zrtYKRa2WQgAh+QQJCwAAACwAAAAAEAALAAAFJGBhGAVgnqhpHIeRvsDawqns0qeN5+y967tYLyicBYE7EYkYAgAh+QQJCwAAACwAAAAAEAALAAAFNiAgjothLOOIJAkiGgxjpGKiKMkbz7SN6zIawJcDwIK9W/HISxGBzdHTuBNOmcJVCyoUlk7CEAAh+QQJCwAAACwAAAAAEAALAAAFNSAgjqQIRRFUAo3jNGIkSdHqPI8Tz3V55zuaDacDyIQ+YrBH+hWPzJFzOQQaeavWi7oqnVIhACH5BAkLAAAALAAAAAAQAAsAAAUyICCOZGme1rJY5kRRk7hI0mJSVUXJtF3iOl7tltsBZsNfUegjAY3I5sgFY55KqdX1GgIAIfkECQsAAAAsAAAAABAACwAABTcgII5kaZ4kcV2EqLJipmnZhWGXaOOitm2aXQ4g7P2Ct2ER4AMul00kj5g0Al8tADY2y6C+4FIIACH5BAkLAAAALAAAAAAQAAsAAAUvICCOZGme5ERRk6iy7qpyHCVStA3gNa/7txxwlwv2isSacYUc+l4tADQGQ1mvpBAAIfkECQsAAAAsAAAAABAACwAABS8gII5kaZ7kRFGTqLLuqnIcJVK0DeA1r/u3HHCXC/aKxJpxhRz6Xi0ANAZDWa+kEAA7"
}
```
the loader is the optional, you can remove it or replacenit with proper loader picture.

and next is html file, it must be an index.html and must contain two script elements of requirements libraries, like this one:
```html
<script type="text/javascript" id="virtual.js"></script>
<script type="text/javascript">
/* anonymous async function */
(async function(){
  /* blog config host file */
  const CONFIG_FILE="hunter.json";
  
  /**
   * prepare for registered files
   * note: do not change the keys
   */
  const REGISTERED_FILES={
    "gaino.js": "https://raw.githubusercontent.com/9r3i/gaino.js/master/gaino.min.js",
    "router.js": "https://raw.githubusercontent.com/9r3i/router.js/master/router.min.js",
    "parser.js": "https://raw.githubusercontent.com/9r3i/parser.js/master/parser.min.js",
    "blog.js": "https://raw.githubusercontent.com/9r3i/blog.js/master/blog.min.js"
  };
  
  /* virtual host file */
  const VIRTUAL_HOST = "https://raw.githubusercontent.com/9r3i/virtual.js/master/virtual.min.js";
  
  /* gaino config -- do not change from this point */
  const GAINO_CONFIG={
    "load": [
      "router.js",
      "parser.js",
      "blog.js"
    ],
    "start": {
      "class": "blog",
      "method": "init",
      "args": [
        CONFIG_FILE
      ]
    }
  };
  
  /* standard virtual initialization -- do not change */
  let vname='virtual.js',
  vtag=document.getElementById(vname),
  vscript=localStorage.getItem('virtual/'+vname);
  if(!vscript){
    vscript=await fetch(VIRTUAL_HOST).then(r=>r.text());
    if(!vscript.match(/function\svirtual/)){
      alert('Error: Failed to load virtual.js');
      return;
    }
  }
  /* execute the virtual script */
  vtag.textContent=vscript;
  /* initialize virtual.js with registered files */
  const app=new virtual(REGISTERED_FILES);
  /* save virtual script */
  app.put(vname,vscript);
  /* load gaino file */
  await app.load('gaino.js');
  /* start the gaino app */
  new gaino(app,GAINO_CONFIG);
  /* doing silent self update for virtual.js */
  app.files[vname]=VIRTUAL_HOST;
  await app.update(vname);
})();
</script>
```
the config file address could be a url.

and also, the html file might be contained a splash screen with your own style. here is the sample:
```html
<style type="text/css">
body{
  margin:0px;
  padding:0px;
}
.index-splash{
  display:flex;
  align-items:center;
  justify-content:center;
  height:100vh;
  width:100vw;
  margin:0px;
  padding:0px;
  font-family:system-ui;
  background-color:#fff;
  background:linear-gradient(#fff 0%,#bdf 80%,#59d 100%);
}
.index-splash progress{
  font-size:24px;
}
.index-splash span{
  position:absolute;
  margin:-35px 0px 0px;
  font-size:13px;
  color:#777;
  animation:fade 2.3s infinite 0s;
}
@keyframes fade{
  0%{opacity:1;}
  50%{opacity:0.3;}
  100%{opacity:1;}
}
</style>
```
and this is in the body:
```html
<div class="index-splash">
<span>Connecting...</span>
<progress max="100"></progress>
</div>
```
the blog.js will using these elements as loader, it detects ```<progress>``` and ```<span>``` elements to put loading information on it.


# sample
and here is a sample page with plain.js
https://relfo.vercel.app/9r3i/plain.js/sample/


# closing
thats all there is to it. Alhamdulillaah...


