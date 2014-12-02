class: center,middle
# gdb

---
class: center,middle
# @hirabaru

---
# gdb とは

The GNU Project Debugger。Linuxに標準的に組み込まれているデバッガ。macにはなかったけど。。

---
# 開始・終了コマンド

 - 開始

  ```
  gdb program名
  ```

 - 終了

  ```
  quit or Ctrl+d
  ```

---
# そもそもgdb入ってるかな？

 - 確認

  ```
  [root@localhost vagrant]# gdb -v
  GNU gdb (GDB) Red Hat Enterprise Linux (7.2-75.el6)
  Copyright (C) 2010 Free Software Foundation, Inc.
  License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
  This is free software: you are free to change and redistribute it.
  There is NO WARRANTY, to the extent permitted by law.  Type "show copying"
  and "show warranty" for details.
  This GDB was configured as "x86_64-redhat-linux-gnu".
  For bug reporting instructions, please see:
  <http://www.gnu.org/software/gdb/bugs/>.
  ```
  
 - もし入ってなかったら。。

  ```
  yum install gdb
  ```

---
# gdbをつかってデバッグするには

 - コンパイル時にデバッグ情報を生成しましょう。
  - コンパイル時に-gオプションを指定

 ```
 [root@localhost C]# gcc -g helloworld.c -o test
 ```

---

 - helloworldをデバッグしてみる

 ```
 [root@localhost C]# gdb test
 ```

 - とりあえず動いた（なんか出たけど。。)

 ```
 (gdb) run
 Starting program: /home/vagrant/C/test
 Hello world!

 Program exited normally.
 Missing separate debuginfos, use: debuginfo-install glibc-2.12-1.132.el6.x86_64
 (gdb)
 ```

---

 - 以下のようなプログラムをデバッグする

```
#include <stdio.h>

int main(int argc, char *argv[]){
    int a;

    for(a=1;a<10;a++){
        printf("This is %d times\n",a);
    }

    return 0;
}
```

---

 - break , next , print

   - break はbreakpointの設定です。break 行、break 関数名といった感じで指定します。
   - next は次の行に移動します。
   - print は変数に入っている値を表示します。 print 変数名といった感じで指定します。

```C
(gdb) break main
Breakpoint 1 at 0x4004d3: file for.c, line 6.
(gdb) r
Starting program: /home/vagrant/C/test

Breakpoint 1, main (argc=1, argv=0x7fffffffe728) at for.c:6
6       for(a=1;a<10;a++){
(gdb) p a
$1 = 0
(gdb) n
7           printf("This is %d times\n",a);
(gdb) p a
$2 = 1
(gdb) n
This is 1 times
6       for(a=1;a<10;a++){

```

---
# その他

 - help

```
 (gdb) h
 List of classes of commands:

 aliases -- Aliases of other commands
 breakpoints -- Making program stop at certain points
 data -- Examining data
 files -- Specifying and examining files
 internals -- Maintenance commands
 obscure -- Obscure features
 running -- Running the program
 stack -- Examining the stack
 status -- Status inquiries
 support -- Support facilities
 tracepoints -- Tracing of program execution without stopping the program
 user-defined -- User-defined commands
 
 Type "help" followed by a class name for a list of commands in that class.
 Type "help all" for the list of all commands.
 Type "help" followed by command name for full documentation.
 Type "apropos word" to search for commands related to "word".
 Command name abbreviations are allowed if unambiguous.
```

---

 - list(現在実行しているプログラムの周辺のソースコードを表示)

```
(gdb) list
1   #include <stdio.h>
2
3   int main(int argc, char *argv[]){
4       int a;
5
6       for(a=1;a<10;a++){
7           printf("This is %d times\n",a);
8       }
9
10      return 0;
```
