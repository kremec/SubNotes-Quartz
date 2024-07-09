Relacije med vhodnimi in izhodnimi besedami [[Končni avtomati|avtomata]] podamo z regularnimi izrazi

Operacije:
- vsota $P+R$  (hkratnost)
  ![[Regularni izrazi-Image-1.png|250]]
- produkt $PR$  (zapovrstnost)
  ![[Regularni izrazi-Image-2.png|350]]
- iteracija $P^*=\{P\}=\lambda+P+PP+ \ ...$
  ![[Regularni izrazi-Image-3.png|80]]

Pravila regularnih izrazov: (vse lahko preverimo z risanjem avtomatov po zgornjih primerih)
- $P+R=R+P$
- $P+(R+Q)=(P+R)+Q$
- $P+P=P$
- $P(RQ)=(PQ)R$
- $(P+R)Q=PQ+RQ$
- $(P^*)^*=P^*$
- $P^*=\lambda + PP^*$
- $P^*P^*=P^*$
- $P^*+P=P^*$

> [!example]- Pretvorba avtomata v regularni izraz
> Gledamo, kako se lahko pomikamo po grafu, možne zanke se predstavi kot iteracije
> ![[Regularni izrazi-Image-4.png|300]]