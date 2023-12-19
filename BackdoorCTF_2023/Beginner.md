I just noted my solves during the CTF

### Beginner-menace
exiftool
flag{7h3_r34l_ctf_15_7h3_fr13nd5_w3_m4k3_al0ng}

### secret_of_j4ck4l
%2525252E%2525252E%2525252Fflag%2525252Etxt
Simple LFI
flag{s1mp13_l0c4l_f1l3_1nclus10n_0dg4af52gav}

### Headache
Correcting magic bytes
flag{sp3ll_15_89_50_4E_47}

### Secret-of-Kurama
JWT secret = "minato" cracked using hashcat
flag{y0u_ar3_tru3_L34F_sh1n0b1_bf56gtr59894}

### Cheat code
XOR 1st & last
```py
v4 = [0]*16
v4[0] = 27
v4[1] = 25
v4[2] = 81
v4[3] = 30
v4[4] = 36
v4[5] = 13
v4[6] = 0
v4[7] = 13
v4[8] = 120
v4[9] = 65
v4[10] = 110
v4[11] = 32
v4[12] = 114
v4[13] = 12
v4[14] = 2
v4[15] = 24
a = "flag{c4n't_HESOY"
b = []
for i in range(16):
  b.append(chr(v4[i]^ord(a[i])))
  print(b,len(b))
  c = ''.join(x for x in b)
  print(c,c[::-1])
print(a+c[::-1])
```
flag{c4n't_HESOYAM_7h15_c4n_y0u}

### Not So Guessy
111010101111011010101110100101
Heads and Tails of 1970 = reverse binary = 985508773 -> Never changed secret
```
Scissors\nRock\nRock\nRock\nScissors\nRock\nPaper\nPaper\nPaper\nRock\nPaper\nScissors\nPaper\nPaper\nRock\nRock\nScissors\nScissors\nRock
```
flag{M0d_0n3_1s_4lw4ys_z3r0}

### Fruits Basket
srand(time(0)) = unix time
```c
#include <stdio.h>
#include <time.h>
int main(){
	unsigned int v3;
	v3 = time(0);
	printf("%d\n",v3);
	srand(v3);
	int i;
	for ( i = 0; i <= 49; ++i ){
		printf("%d",rand()%10);
	}
	//printf("%d",rand()%10);
	printf("\n");
	return 0;
}
```
```py
a = ["Apple","Orange","Mango","Banana","Pineapple","Watermelon","Guava","Kiwi","Strawberry","Peach"]
b = input().strip("\n")
for i in range(len(b)):
	print(a[int(b[i])])
```
```
$ gcc lol.c -o lol
$ ./lol && nc -nv 34.70.212.151 8006
1702899079
29274954304636195338411698984496315011463846755211
(UNKNOWN) [34.70.212.151] 8006 (?) open
There is a basket full of fruits, guess the fruit which I am holding ...
This seems hard, so I will give an awesome reward, something like a shell if you guess all the fruits right :)

The game starts now !
1
Your guess :
```
```
$ # In another shell
$ python3 fruitbasket.py
29274954304636195338411698984496315011463846755211 -> given as input
Apple
Strawberry
...
$ # Copy the above output and just paste it in the netcat session to get the remote shell.
```
flag{fru17s_w3r3nt_r4nd0m_4t_a11}
