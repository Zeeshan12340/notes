# XOR
When XORing values in python, always remember to convert raw strings to bytes (bytes are considered as type ints in python and also, hex characteres `0x0e` are also type-set as ints

```text-plain
secret = b"infloop\0"

key = [
  0x00, 0x0e, 0x05, 0x03,
  0x1c, 0x06, 0x12, 0x71,
  0x1e, 0x1b, 0x14, 0x12,
  0x16, 0x13, 0x0c, 0x7b
]

password = ""

for i in range(16):
    password += chr(key[i] ^ (secret[i % len(secret)] + i))

print(f"{password = }")
```