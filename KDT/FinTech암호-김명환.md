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

$$ \varphi(n) := \sum_{\substack{1\le k \le n \\ (k,n)=1}} 1 = \sideset{}{'}\sum_{k=1}^{n} 1$$

여기서

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

## 2025-07-08

[Modular arithmetic - Wikipedia](https://en.wikipedia.org/wiki/Modular_arithmetic)

[기약잉여계](https://en.wikipedia.org/wiki/Reduced_residue_system)

[FLiT](https://en.wikipedia.org/wiki/Fermat%27s_little_theorem) ${ p \in \mathbb{P} }$, ${ a \in \mathbb{Z} }$, ${ p \nmid a }$

$$ a^{p-1} \equiv 1 \pmod{p} $$
**Proof)** ${ \mathbb{Z}^{\ast}_{p} }$와 ${a \mathbb{Z}^{\ast}_{p} }$의 원소들은 mod p로 같은 것끼리 일대일대응.

$$ \therefore a^{p-1}(p-1)!=\prod_{i=1}^{p-1} ai \equiv \prod_{i=1}^{p-1} i = (p-1)!\pmod{p} $$

소거정리에 의해,

$$ a^{p-1} \equiv 1 \pmod{p} $$

[Euler's Generalization of FLiT](https://en.wikipedia.org/wiki/Euler%27s_theorem)

$$ \gcd(a,m) = 1 \implies a^{\varphi(m)} \equiv 1 \pmod{m} $$

법 m에 대한 a의 위수

$$ \min \left\{ d \in \mathbb{Z} : a^{d} \equiv 1 \pmod{m} \right\}  $$

생성근(primitive roots)

${ m }$과 서로소인 ${ g }$에 대하여, ${ \operatorname{ord}_{m}(g)=\varphi(m) }$일 때 g를 ==법 m에 대한 생성근==이라고 한다.

암호 체계: 순서쌍 ${ (\mathbf{P},\mathbf{C}, \mathbf{K}, \mathrm{Enc}, \mathrm{Dec}) }$
- ${ \mathbf{P}}$: 유한개의 평문 집합
- ${ \mathbf{C} }$: 유한개의 암호문 집합
- ${ \mathbf{K} }$: 유한개의 키 집합 (키 공간)
- Enc: 암호화 알고리듬
- Dec: 복호화 알고리듬

${ \forall K \in \mathbf{K} }$, ${ \exists K' \in \mathbf{K} }$: ${ K }$와 ${ K' }$에 대응되는 두 함수 ${ \mathrm{Enc}_{K}: \mathbf{P}\to \mathbf{C} }$, ${ \mathrm{Dec}_{K'}:\mathbf{C}\to \mathbf{P} }$는 임의의 평문 ${ x \in \mathbf{P} }$에 대하여, 다음을 만족한다.

$$ \mathrm{Dec}_{K'}(\mathrm{Enc}_{K}(x)) = x $$

- 비밀(대칭) 키 암호: ${ K = K' }$
- 공개(비대칭) 키 암호: ${ K \neq K' }$

[Public-key cryptography - Wikipedia](https://en.wikipedia.org/wiki/Public-key_cryptography)
[One-way function - Wikipedia](https://en.wikipedia.org/wiki/One-way_function)
[RSA cryptosystem - Wikipedia](https://en.wikipedia.org/wiki/RSA_cryptosystem)

기존 암호는 키를 미리 공유를 해야 되어서 골치가 아팠는데, RSA가 나오고 공개키 암호가 시장을 장악해버림.

1. 큰 소수 p와 q를 선택한 다음 n=pq를 계산
2. ${ \varphi(n) = (p-1)(q-1) }$과 서로소인 e를 선택한 다음 ${ ed \equiv 1 \pmod{\varphi(n)} }$을 만족하는 d를 계산 (${ 1<e,d<\varphi(n)) }$
3. n, e는 공개하고 ${ p,q,\varphi(n),d }$ 비밀. e: 암호화키, ${ d }$: 복호화 키
4. ${ \mathbf{P}=\mathbf{C}=\mathbb{Z}_{n}^{\times} }$; ${ \mathbf{K}= \mathbb{Z}_{\varphi(n)}^{\ast} }$

[Miller–Rabin primality test - Wikipedia](https://en.wikipedia.org/wiki/Miller%E2%80%93Rabin_primality_test)

RSA는 길이가 길어지면 오래걸린다.

비밀키 방식과 RSA의 결합

비밀 키 방식을 쓰는데 키를 RSA로 암호화 해서 교환.

[Linear congruential generator - Wikipedia](https://en.wikipedia.org/wiki/Linear_congruential_generator)

## 연습문제

93p. 27
216p. 13, 15