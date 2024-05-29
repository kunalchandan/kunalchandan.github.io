---
title: AMD Systems Interview
categories: [interviews]
tags: [interview, amd, software]
author: kchandan
math: true
---


# Round 1
Interview with hiring manager Ava Shui.

```c
// hello!
// 0x100 = 5

int* ptr = 0x100;
ptr* = 5;

// 5 -> 2 (b101)
int count1s (int x) {
	int count = 0;
  while (x != 0) {
  	count += (x & 0b1);
    x = (x>>1);
	}
  return count;
}

// Count stored at rega
// rega
// regb stores x

addi rega, zero, 0
// return count here if x == 0
while_label:
// temp is regc
andi regc, regb, 0x1
add rega, rega, regc
srri regb, regb, 0x1
bnq regb, reg0, while_label


BASE_ADDR=0xC500_0000
Reg0…
Reg1…
Reg2 Errors (RW1C)
	- [31:28] Rsvd (default 0)
	- [27] Correctable error detected
	- [26] Non-Fatal error detected
	- [25] Fatal error detected
	- [24] Unsupported request detected
	- [23:4] Rsvd (default 0)
	- [3] Slave completion overflow
	- [2] Unexpected completion
	- [1] Timeout detected
	- [0] Rsvd (default 0)

// Write a function in C, to check if any errors are logged in Reg2 and clear any that are (note: RW1C)

bool errors_detected() {
	int* reg2 = 0xC500_0000 + (2*4);
    bool errors_detected = false;
    int flag_bits = 0x0F0000E;
    int bad_error_flag_bits = 0x070000E;
    errors_detected = bad_error_flag_bits & *reg2; // detect errors
    reg2* = *reg2 & flag_bits;
    return errors_detected;
}
```
