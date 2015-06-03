# [Using GNU C __attribute__](http://www.unixwiz.net/techtips/gnu-c-attributes.html)
GUN C中最好的功能之一就是`__attribute__`机制(但是鲜有人知),它允许开发人员附加独特的函数声明使得编译时能够执行更仔细的
错误检测。它设计目的是能与非GNU兼容，并且我们已经在可移植代码上使用了许多年而且效果显著。

需要注意的是`__attribute__`拼写是两个前下划线和两个后下划线，通常在内容的周围有两层括号。有一个很好的理由解释这个原因
-看下文。Gnu CC需要使用_-Wall_编译指令使它生效(是的,警告的精细程度可以控制，无论如何我们有多少的警告(FIXME:这句不理解))。
## `__attribute__format`
这个`__attribute__`允许复制类**printf**或者类**scanf**函数特殊的去声明函数，这使编译器检测整个代码参数的格式字符串。这是在
跟踪难以发现的错误时是非常有帮助的。

有两种形式：
* `__attribute__((format(printf,m,n)))`
* `__attribute__((format(scanf,m,n)))`

但在实践过程中我们更多的用到第一种形式。
这`(m)`是格式字符串的参数个数，而`(n)`是这第一个可变参数的参数号
>
>/* like printf() but to standard error only */  
> extern void eprintf(const char *format, ...)  
>	`__attribute__`((format(printf, 1, 2)));  /* 1=format 2=params */   
>  
> /* printf only if debugging is at the desired level */  
> extern void dprintf(int dlevel, const char *format, ...)  
>	`__attribute__`((format(printf, 2, 3)));  /* 2=format 3=params */  
>

当函数这样声明时，编译器就会检查参数列表
>$ cat test.c   
1  extern void eprintf(const char *format, ...)   
2               __attribute__((format(printf, 1, 2)));  
3  
4  void foo()  
5  {  
6      eprintf("s=%s\n", 5);             /* error on this line */  
7  
8      eprintf("n=%d,%d,%d\n", 1, 2);    /* error on this line */  
9  }  
>  
$ cc -Wall -c test.c  
test.c: In function `foo':  
test.c:6: warning: format argument is not a pointer (arg 2)  
test.c:8: warning: too few arguments for format   
>  
请注意“标准”的库函数-类似printf函数-早已被编译器默认识别。

## __attribute__noreturn
