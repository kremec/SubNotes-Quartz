## Binarni številski sistem
### Pretvorbe v binarnem sistemu
- Pretvorba $n$-mestnega binarnega števila v desetiško:
$$
A=\sum_{i=0}^{n-1}a_i2^i
$$
- Pretvorba binarnega števila z $n$ celimi in $m$ decimalnimi mesti:
$$
A=\sum_{i=-m}^{n-1}a_i2^i
$$
### Dvojiški komplement
Binarno število negiramo in mu prištejemo $1$
- Pretvorba binarnega števila $n$ v dvojiškem komplementu v desetiško:
$$
A=-a_{n-1}2^{n-1}+\sum_{i=-m}^{n-2}a_i2^i
$$
V binarnem dvojišme komplementu lahko z $n$ mesti zapišemo decimalna števila v razponu $-2^{n-1}\le A \le 2^{n-1}-1$
### Pomik v levo ali desno
- Pomik v levo za $n$ mest $\rightarrow$ množenje števila z $2^n$
- Pomik v desno za $n$ mest $\rightarrow$ deljenje števila z $2^n$