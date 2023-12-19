### Secret Door

Open the provided chall.out in any tool of your choice, being the noob I am, I uploaded it on https://dogbolt.org for multiple decompilation results and continued with hex rays decompiled code since it was easier for me.

```c
__int64 __fastcall func_1(char a1, char a2)
{
  _BYTE *v2; // rax
  _BYTE *v3; // rax
  __int64 v4; // rbx
  const char *v5; // rsi
  char v7; // [rsp+1Bh] [rbp-485h] BYREF
  int i; // [rsp+1Ch] [rbp-484h]
  __int64 v9[2]; // [rsp+20h] [rbp-480h] BYREF
  __int64 v10[2]; // [rsp+30h] [rbp-470h] BYREF
  __int64 v11[4]; // [rsp+40h] [rbp-460h] BYREF
  char v12[32]; // [rsp+60h] [rbp-440h] BYREF
  char v13[512]; // [rsp+80h] [rbp-420h] BYREF
  _QWORD v14[67]; // [rsp+280h] [rbp-220h] BYREF

  v14[65] = __readfsqword(0x28u);
  std::allocator<char>::allocator(v11);
  std::string::basic_string<std::allocator<char>>((__int64)v12, "encoded.bin", (__int64)v11);
  std::allocator<char>::~allocator(v11);
  std::ifstream::basic_ifstream(v14, v12, 4LL);
  std::allocator<char>::allocator(&v7);
  std::istreambuf_iterator<char>::istreambuf_iterator((__int64)v10);
  std::istreambuf_iterator<char>::istreambuf_iterator((__int64)v9, v14);
  std::vector<char>::vector<std::istreambuf_iterator<char>,void>(v11, v9[0], v9[1], v10[0], v10[1], (__int64)&v7);
  std::allocator<char>::~allocator(&v7);
  for ( i = 0; i <= 90245; ++i )
  {
    if ( (i & 1) != 0 )
    {
      v3 = (_BYTE *)std::vector<char>::operator[](v11, i);
      *v3 ^= a2;
    }
    else
    {
      v2 = (_BYTE *)std::vector<char>::operator[](v11, i);
      *v2 ^= a1;
    }
  }
  std::ofstream::basic_ofstream(v13, "the_door.jpg", 4LL);
  v4 = std::vector<char>::size(v11);
  v5 = (const char *)std::vector<char>::data(v11);
  std::ostream::write((std::ostream *)v13, v5, v4);
  std::ofstream::close(v13);
  std::ofstream::~ofstream(v13);
  std::vector<char>::~vector((__int64)v11);
  std::ifstream::~ifstream(v14);
  std::string::~string(v12);
  return 0LL;
}
// 2340: using guessed type __int64 __fastcall std::ifstream::~ifstream(_QWORD);
// 23C0: using guessed type __int64 __fastcall std::string::~string(_QWORD);
// 2480: using guessed type __int64 __fastcall std::allocator<char>::~allocator(_QWORD);
// 2490: using guessed type __int64 __fastcall std::ofstream::basic_ofstream(_QWORD, _QWORD, _QWORD);
// 2520: using guessed type __int64 __fastcall std::ofstream::close(_QWORD);
// 2550: using guessed type __int64 __fastcall std::ofstream::~ofstream(_QWORD);
// 2580: using guessed type __int64 __fastcall std::ifstream::basic_ifstream(_QWORD, _QWORD, _QWORD);
// 25C0: using guessed type __int64 __fastcall std::allocator<char>::allocator(_QWORD);
// 26E9: using guessed type __int64 var_460[4];

//----- (00000000000029D1) ----------------------------------------------------
_BOOL8 __fastcall func_2(int *a1)
{
  return *a1 == 78
      && a1[1] != (*a1 == 15)
      && a1[2] == 120
      && a1[3] != (a1[2] == 31)
      && a1[4] == 120
      && a1[5] != (a1[4] == 11)
      && a1[6] == 116
      && a1[6] != (a1[7] == 6)
      && a1[8] == 100
      && a1[9] != (a1[8] == 33)
      && a1[10] == 99
      && a1[11] != (a1[10] == 34)
      && a1[12] == 120
      && a1[13] == a1[12]
      && a1[14] == 114
      && a1[15] == a1[14] + 1
      && a1[16] == 33;
}

//----- (0000000000002B8F) ----------------------------------------------------
__int64 __fastcall func_3(__int64 a1, __int64 a2)
{
  int i; // [rsp+14h] [rbp-Ch]
  __int64 v4; // [rsp+18h] [rbp-8h]

  v4 = operator new[](0x44uLL);
  for ( i = 0; i <= 16; ++i )
    *(_DWORD *)(4LL * i + v4) = *(char *)std::string::operator[](a2, i) ^ *(_DWORD *)(4LL * i + a1);
  return v4;
}
// 24B0: using guessed type __int64 __fastcall std::string::operator[](_QWORD, _QWORD);

//----- (0000000000002C13) ----------------------------------------------------
__int64 __fastcall func_4(__int64 a1, __int64 a2)
{
  unsigned __int64 i; // [rsp+18h] [rbp-18h]
  unsigned __int64 v4; // [rsp+20h] [rbp-10h]
  __int64 v5; // [rsp+28h] [rbp-8h]

  v4 = std::string::size(a1);
  v5 = operator new[](0x44uLL);
  for ( i = 0LL; i < v4; ++i )
    *(_DWORD *)(v5 + 4 * i) = (char)(*(_BYTE *)(a2 + i) ^ *(_BYTE *)std::string::operator[](a1, i));
  return v5;
}
// 23E0: using guessed type __int64 __fastcall std::string::size(_QWORD);
// 24B0: using guessed type __int64 __fastcall std::string::operator[](_QWORD, _QWORD);

//----- (0000000000002CA4) ----------------------------------------------------
__int64 __fastcall func_5(__int64 a1, __int64 a2)
{
  int v2; // ebx
  _BYTE *v3; // rax
  char v4; // bl
  _BYTE *v5; // rax
  __int64 v6; // rbx
  char v8; // [rsp+1Bh] [rbp-55h] BYREF
  int v9; // [rsp+1Ch] [rbp-54h]
  int i; // [rsp+20h] [rbp-50h]
  int j; // [rsp+24h] [rbp-4Ch]
  _BYTE *v12; // [rsp+28h] [rbp-48h]
  char v13[40]; // [rsp+30h] [rbp-40h] BYREF
  unsigned __int64 v14; // [rsp+58h] [rbp-18h]

  v14 = __readfsqword(0x28u);
  v9 = 0;
  for ( i = 0; i <= 16; ++i )
  {
    v2 = *(char *)std::string::operator[](a1, i);
    v9 += v2 + *(char *)std::string::operator[](a2, i);
  }
  v3 = (_BYTE *)operator new(1uLL);
  *v3 = 0;
  v12 = v3;
  std::allocator<char>::allocator(&v8);
  std::string::basic_string<std::allocator<char>>((__int64)v13, "R{{xqpMuYu`qKLPLP", (__int64)&v8);
  std::allocator<char>::~allocator(&v8);
  for ( j = 0; j <= 16; ++j )
  {
    v4 = v9 + 46;
    v5 = (_BYTE *)std::string::operator[](v13, j);
    v12[j] = v4 ^ *v5;
  }
  v6 = (__int64)v12;
  std::string::~string(v13);
  return v6;
}
// 23C0: using guessed type __int64 __fastcall std::string::~string(_QWORD);
// 2480: using guessed type __int64 __fastcall std::allocator<char>::~allocator(_QWORD);
// 25C0: using guessed type __int64 __fastcall std::allocator<char>::allocator(_QWORD);
// 25F0: using guessed type __int64 __fastcall std::string::operator[](_QWORD, _QWORD);

//----- (0000000000002E0F) ----------------------------------------------------
__int64 __fastcall add_of_chars(char *a1)
{
  unsigned int v2; // [rsp+10h] [rbp-8h]
  int i; // [rsp+14h] [rbp-4h]

  v2 = 0;
  for ( i = 0; i <= 16; ++i )
    v2 += a1[i];
  return v2;
}

//----- (0000000000002E50) ----------------------------------------------------
int __fastcall main(int argc, const char **argv, const char **envp)
{
  __int64 v3; // rax
  char v5; // [rsp+13h] [rbp-EDh] BYREF
  int v6; // [rsp+14h] [rbp-ECh]
  int *v7; // [rsp+18h] [rbp-E8h]
  char v8[32]; // [rsp+20h] [rbp-E0h] BYREF
  char v9[32]; // [rsp+40h] [rbp-C0h] BYREF
  char v10[32]; // [rsp+60h] [rbp-A0h] BYREF
  char v11[32]; // [rsp+80h] [rbp-80h] BYREF
  int v12[18]; // [rsp+A0h] [rbp-60h]
  unsigned __int64 v13; // [rsp+E8h] [rbp-18h]

  v13 = __readfsqword(0x28u);
  if ( argc != 2 )
  {
    std::operator<<<std::char_traits<char>>(&std::cout, "Just try to get the door");
    exit(0);
  }
  if ( strlen(argv[1]) != 17 )
  {
    std::operator<<<std::char_traits<char>>(&std::cout, "that's not even a door :p");
    exit(0);
  }
  v6 = 0;
  std::string::basic_string(v8);
  v12[0] = 66;
  v12[1] = 119;
  v12[2] = 101;
  v12[3] = 113;
  v12[4] = 123;
  v12[5] = 98;
  v12[6] = 114;
  v12[7] = 125;
  v12[8] = 119;
  v12[9] = 89;
  v12[10] = 115;
  v12[11] = 125;
  v12[12] = 111;
  v12[13] = 109;
  v12[14] = 62;
  v12[15] = 1;
  v12[16] = 0;
  while ( v6 <= 16 )
  {
    std::string::push_back(v8, (unsigned int)(char)(LOBYTE(v12[v6]) ^ (v6 + 17)));
    ++v6;
  }
  std::allocator<char>::allocator(&v5);
  std::string::basic_string<std::allocator<char>>((__int64)v9, "ThatsHardcoded!!!", (__int64)&v5);
  std::allocator<char>::~allocator(&v5);
  std::string::basic_string(v11, v9);
  std::string::basic_string(v10, v8);
  func_5((__int64)v10, (__int64)v11);
  std::string::~string(v10);
  std::string::~string(v11);
  v7 = (int *)operator new[](0x44uLL);
  v3 = func_4((__int64)v8, (__int64)argv[1]);
  v7 = (int *)func_3(v3, (__int64)v9);
  if ( func_2(v7) )
    func_1(*v7, v7[16]);
  else
    std::operator<<<std::char_traits<char>>(&std::cout, "Wrong door");
  std::string::~string(v9);
  std::string::~string(v8);
  return 0;
}
```

I spent hours trying to reverse it, supplying the right input etc.

Then I was just drooling over func_1 then realized that if the correct input is given, the this function just uses a variation of that input to decode the encoded.bin to the_door.jpg using 🥁🥁🥁 **XOR**. 😭

I then used the magic bytes of jpg (`FFD8FFE000104A4649460001`) as the XOR key and decoded the encoded.bin in cyberchef.

![image](https://github.com/suds4131/CTF-Writeups/assets/128071555/67c930b1-c59d-4698-b6dd-8e7a0d16f5f0)


Checking the output, we see that `N!` is repeated about the key, that means `N!` is the original key.

![image](https://github.com/suds4131/CTF-Writeups/assets/128071555/db8fa783-ba51-4fd9-8f1f-8a230491d431)

Then saving and viewing the jpg file gives us the flag.

![secret-door](https://raw.githubusercontent.com/suds4131/CTF-Writeups/main/BackdoorCTF_2023/Rev/download.jpg)

### Flag

`flag{0p3n3d_7h3_s3cr3t_r3d_d00r}`
