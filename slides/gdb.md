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
