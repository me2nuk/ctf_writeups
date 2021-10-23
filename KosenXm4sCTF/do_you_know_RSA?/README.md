# do_you_know_RSA?:Crypto:78pts
RSA暗号機を作ってみたよ！ えーと、、、公開鍵を公開して、、、秘密鍵を隠して、、、、 、、あれ？この情報って表示していいんだっけ？  
[param.txt](param.txt)  

# Solution
param.txtが配布されている。  
```text:param.txt
N = 872466878637044085809546928077402525188932163354013071311247
p = 1202641222143185422372899516011
E = 65537
crypted message is 736752258923832368359268459529023058483734448152703465168101
```
RSAを復号するだけのようだ。  
q(n/p)は725458983588015524409059834477となる([factordb.com](http://factordb.com/index.php?query=872466878637044085809546928077402525188932163354013071311247))。  
以下のrsa.pyで行う。  
```python:rsa.py
from Crypto.Util.number import *

n = 872466878637044085809546928077402525188932163354013071311247
p = 1202641222143185422372899516011
e = 65537
c = 736752258923832368359268459529023058483734448152703465168101

q = 725458983588015524409059834477

phin = (p-1)*(q-1)
d = inverse(e, phin)
m = pow(c, d, n)
print(long_to_bytes(m))
```
実行する。  
```bash
$ python rsa.py
b'xm4s{dont_leak_p_and_q!!}'
```
flagが得られた。  

## xm4s{dont_leak_p_and_q!!}