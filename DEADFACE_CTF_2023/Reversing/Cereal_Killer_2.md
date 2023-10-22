### Cereal Killer 2

Disassembly in ghidra.

```C
void decode_str(int param_1,int param_2,int param_3,int param_4)

{
  int local_10;
  int local_c;
  
  local_10 = 0;
  local_c = 0;
  while (local_c < param_2) {
    *(byte *)(param_4 + local_c) = *(byte *)(param_3 + local_c) ^ *(byte *)(param_1 + local_10);
    local_c = local_c + 1;
    local_10 = local_10 + 1;
    if (0xb < local_10) {
      local_10 = 0;
    }
  }
  *(undefined *)(param_4 + local_c) = 0;
  return;
}

undefined4 main(void)

{
  int iVar1;
  undefined4 uVar2;
  int in_GS_OFFSET;
  char local_2014 [4096];
  char local_1014 [4096];
  int local_14;
  undefined *local_10;
  
  local_10 = &stack0x00000004;
  local_14 = *(int *)(in_GS_OFFSET + 0x14);
  puts("Luciafer also loves Halloween, so she, too, LOVES SPOOKY CEREALS!");
  puts("She has different favorite villain from 70-80\'s horror movies.");
  printf("What is Luciafer\'s favorite breakfast cereal? ");
  fgets(local_2014,0xfff,_stdin);
  decode_str(local_2014,0x3f,&DAT_00012094,local_1014);
  iVar1 = strncmp(local_1014,"CORRECT!!!!!",0xc);
  if (iVar1 == 0) {
    puts(local_1014);
  }
  else {
    printf("%s",
           "INCORRECT....: I\'m afraid that is not Lucia\'s current favorite monster cereal.  She is  kind of capricious, you know, so it changes often.\n"
          );
  }
  uVar2 = 0;
  if (local_14 != *(int *)(in_GS_OFFSET + 0x14)) {
    uVar2 = __stack_chk_fail_local();
  }
  return uVar2;
}
```

According to `iVar1 = strncmp(local_1014,"CORRECT!!!!!",0xc)`, we should get `local_1014` as the `CORRECT!!!!!` string for check to pass.
Decode_str is xoring our input i.e., `local_2014` with some data `&DAT_00012094` and seems to keep repeating the key after every 0xb xors'.(Cycling through the key)

Since,
input ^ data = "CORRECT!!!!!"
thus,
data ^ "CORRECT!!!!!" = input

```python3
>>> from pwn import xor
>>> a = bytes.fromhex('083D333F1536324752121B656B48410B3C14011D34415B291B134C2602342B160640170D385F22023D1C084B355C48690F134C2F31114B2D1A5749656A531C')
>>> xor(a, "CORRECT!!!!!")
b"KramPuffs3:D(\x07\x13YyWU<\x15`z\x08X\\\x1etGw\x7f7'a6,{\x10pPx_\\j\x14}iHL\\\x1e}tR\x1f\x0c;vhD)\x1cN"
```
The first 12 bytes is the password, i.e., `KramPuffs3:D`.
```python3
>>> xor(a, "KramPuffs3:D")
b'CORRECT!!!!! : flag{GramPa-KRAMpus-Is-Comin-For-Da-Bad-Kids!!!}'
```

### Flag
`flag{GramPa-KRAMpus-Is-Comin-For-Da-Bad-Kids!!!}`
