## add

### C

```c
// foo.c
long long add(long long a, long long b) { return a + b; }
```

### LLVM IR

```llvm
; clang -emit-llvm -S foo.c -O0
; Simplified LLVM IR
; foo.ll
define i64 @add(i64 %0, i64 %1) {
  %3 = alloca i64, align 8
  %4 = alloca i64, align 8
  store i64 %0, ptr %3, align 8
  store i64 %1, ptr %4, align 8
  %5 = load i64, ptr %3, align 8
  %6 = load i64, ptr %4, align 8
  %7 = add nsw i64 %5, %6
  ret i64 %7
}
```



```llvm
; clang -emit-llvm -S foo.c -O3
; Simplified LLVM IR
; foo.ll
define i64 @add(i64 %0, i64 %1) {
  %3 = add nsw i64 %1, %0
  ret i64 %3
}
```

### RISCV

```asm
add:
	add	a0, a0, a1
	ret
```

