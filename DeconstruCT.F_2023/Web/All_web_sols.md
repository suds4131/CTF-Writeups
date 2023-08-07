Since the CTF isn't live now I can't deploy machines so I will share what I remember I used to solve the web challs.

### Sweet-Nothing
Description: What can be sweeter than doing nothing? The flag is right in front of you.
Solution: -
There were an Italian flag and things related to Italy in the index of the website.
So we change the `Accept-Language` Header to include `it-IT`.
```
Accept-Language: it-IT
```
We get a resopnse saying that the query `secret` is `spaghetti`. So we set the URL query as so along with the changed language header.
```
https://chall.web/?secret=spaghetti
```

### why-are-types-weird
Description: Jacob is making a simple website to test out his PHP skills. He is certain that his website has absolutely zero security issues.
Solution: - 
This was a PHP type juggling chall.
Upon viewing the html source of the index, we see that `source.php` is commented and upon visiting source.php we get the login.php source code.
It had a weak comparision in place.
Similar to below.
```php
<?php
if (password_hash($_GET['password'],'sha1') == "0") {
  header("Location: admin.php")
}
?>
```
So I went down to John Hammond's [ctf-katana](https://github.com/JohnHammond/ctf-katana#php) and pulled out some SHA1 magic hashes and their plaintext and used them as password along with "admin" as username.
In admin.php you can search for user based on ID, its basic Union Based SQLi to extract info from another table.

### debugzero
Description: Someone on the dev team fat fingered their keyboard, and deployed the wrong app to production. Try and find what went wrong. The flag is in a file called "flag.txt"
Solution: -
A html comment in the index read something like `John, how many times do I tell you to turn off debug mode in production.` So I immediately tried the most possible thing and that is `/console`. We could also fuzz directories using big.txt from dirb, we would have gotten it.
And the PIN to the locked console was present in `styles/style.css` which could be seen in HTML source.

### gitcha
Description: Simon is maintaining a personal portfolio website, along with a secret which no one else knows. Can you discover his secret?
Solution: -
The website had its `.git` exposed. I used `git-dumper` to dump it.
Checking up `robots.txt` reveals to us a `/supersecret/` which can be accessed only if a specific cookie is set. We can learn about this by reviewing the .git dump.
```node
const express = require("express");
const fs = require("fs");
const serveIndex = require("serve-index");
const cookieParser = require("cookie-parser");
const nunjucks = require("nunjucks");
const bodyParser = require("body-parser");

const { PrismaClient } = require("@prisma/client");
const prisma = new PrismaClient();

const app = express();

const checkAdmin = (req, res) => {
  if (req.cookies["SECRET_COOKIE_VALUE"] === "thisisahugesecret") {
    return true;
  }
  return false;
};

nunjucks.configure("views", {
  autoescape: true,
  express: app,
});

app.use(cookieParser());
app.use(express.static("public"));
app.use(bodyParser.urlencoded({ extended: true }));

app.use("/.git", express.static(".git/"), serveIndex(".git/", { icons: true }));

app.get("/robots.txt", (req, res) => {
  res.type("text/plain");
  res.send("User-agent: *\nDisallow: /.git/\nDisallow: /supersecret/");
});

app.get("/supersecret", async (req, res) => {
  if (checkAdmin(req, res)) {
    const results = await prisma.note.findMany();
    res.render("notes.html", { foo: "bar", notes: results });
  } else {
    res.redirect("/");
  }
});

app.get("/getnotedetails", async (req, res) => {
  if (checkAdmin(req, res)) {
    const { id } = req.query;
    const note = await prisma.note.findUnique({ where: { id: parseInt(id) } });
    res.send(
      nunjucks.renderString(`
      <div style="margin: 15px;">
        <h1 style="font-family: Roboto;">${note.title}</h1>
        <p>${note.content}</p>
      </div>
  `)
    );
  } else {
    res.redirect("/");
  }
});

app.post("/addnote", async (req, res) => {
  if (checkAdmin(req, res)) {
    await prisma.note.create({
      data: {
        title: req.body.title,
        content: req.body.content,
      },
    });
    res.status(200).send("Note added");
  } else {
    res.status(403).send("Forbidden");
  }
});

app.get("/viewsource", (req, res) => {
  if (checkAdmin(req, res)) {
    const data = fs.readFileSync("index.js", "utf8");
    res.type("text/javascript");
    res.send(`
        ${data}
    `);
  }
});

app.listen(8080, () => {
  console.log("Example app listening on port 8080!");
});
```
According to the above, we set cookie as `SECRET_COOKIE_VALUE=thisisahugesecret` which gives us access to the supersecret directory.
We can see that the `/getnotedetails` is vulnerable to SSTI. I used [this blog](http://disse.cting.org/2016/08/02/2016-08-02-sandbox-break-out-nunjucks-template-engine) as reference.
```
{{range.constructor("return global.process.mainModule.require('child_process').execSync('cat flag.txt')")()}}
```
Thus creating a note with above payload as title/content and viewing the note gets us code execution via SSTI.

### where-are-the-cookies
?? I forgot this.

