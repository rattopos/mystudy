# 핀테크와 암호

SKT 사건 전에 암호학자들이 해킹은 근본적으로 막기 어려우니 암호화 해서 보관하라고 경고함 하지만 듣질 않음.

암호의 90% 이상은 가족 생년월일이나 전화번호

암호문을 도청한 도청자가,
기밀성: 평문을 알 수 없어야하고
효율성: 값싸고(빠르고) 편리하며
무결성: 변조가 불가능하고 오류도 적어야

비밀키 암호화 키체계의 약점: 주기적으로 공유해야됨

1970년대 이전에는 모두 비밀키 암호였음.

[Kerckhoffs's principle - Wikipedia](https://en.wikipedia.org/wiki/Kerckhoffs%27s_principle)

고전 암호: 20세기 초, 전신이 발명되기 전까지의 암호
- [Scytale - Wikipedia](https://en.wikipedia.org/wiki/Scytale)
- [Atbash - Wikipedia](https://en.wikipedia.org/wiki/Atbash)
- [Caesar cipher - Wikipedia](https://en.wikipedia.org/wiki/Caesar_cipher)
[빈도수 공격](https://en.wikipedia.org/wiki/Frequency_analysis)에 뚫림

근대 암호: 전신의 발명 이후부터 제2차세계대전 종전까지의 암호
- 복잡한 암/복호화 기계를 사용함으로써 해독에 엄청난 계산이 필요(기계암호)
- Enigma, TypeX, Hagelin, SIGABA, Purple
- 기계 암호의 해독을 위해 전자계산기 개발 → 컴퓨터

현대 암호: 제2차 세계대전 종전 이후부터
- Shannon의 이론("통신의 수학적 이론")
- 컴퓨터의 눈부신 발달
- 고급 수학 이론의 활용, 수리암호론으로 불림.

민수용 암호의 등장
- 전자 상거래, 인터넷 뱅킹, 암호화폐/블록체인, 서명/인증 등

## 2025-07-07

$$ a \mid b \iff b = ac $$

나머지 정리: ${ a,b \in \mathbb{Z},\, b \neq 0 }$, ${ \exists! q,r \in Z,\, 0\le r< \left\lvert b \right\rvert }$

$$ a = bq + r $$

최대공약수

${ a,b \in \mathbb{Z},\, ab \neq 0 }$

$$ \gcd(a,b) := \max \left\{ d \in \mathbb{N}^{\ast} : d \mid a \text{ and } d \mid b \right\}  $$

최대 공약수 정리

$$ \gcd(a,b) = d \implies (\exists x,y \in \mathbb{Z})\ ax + by = d $$

[Integer factorization - Wikipedia](https://en.wikipedia.org/wiki/Integer_factorization)


$$ d(n) := \sum_{d \mid n} 1 $$

$$ \sigma(n) := \sum_{d \mid n} d  $$

$$ \varphi(n) := $$

$$ a \equiv b \pmod{m} \iff a -b = km $$

소거정리

$$ ac \equiv bc \pmod{m} \implies a \equiv b \pmod{m/d} $$

${ \gcd(c,m) = 1 }$이면,

$$ cx + dy = 1 $$
을 만족하는 해 ${ x,y }$가 존재하고

$$ cx \equiv 1 \pmod{m} $$

이때 ${ x }$는 유일하다:

$$ cx_{1} \equiv c x_{2} \pmod{m} \stackrel{\text{소거정리}}{\implies} x_{1} \equiv x_{2} \pmod{m} $$

**법 ${ m }$에 대한 ${ c }$의 역수**라고 하고 이를 ${ c^{\ast} \pmod{m} }$로 표기.


