Matroid



정의 1. matroid $\mathcal{M} = (S,  \mathcal{I})$ 에서 $S$는 유한집합, $ \mathcal{I} \subset 2^S$ 는 독립집합(independent set)들의 collection이다. 이 때, $I$는 다음 세 가지 조건을 만족하여야 한다.

1. $\phi \in  \mathcal{I}$
2. $Y \subset X, X \in  \mathcal{I} \Rightarrow Y \in  \mathcal{I}$ 
3. $X, Y \in  \mathcal{I}, |X| < |Y|$ 이면 $X + y \in  \mathcal{I}$ 를 만족하는 $y \in Y \setminus X$가 존재



매트로이드는 다양한 집합에서 정의될 수 있다. 그 중 대표적인 예 몇 가지를 살펴보자.

예시 1. Vector matroid

체 $\mathbb{F}$ 상에서 정의된 $m \times n$ 행렬 $A$을 생각하자. $v_i$를 $A$의 $i$번째 column vector라 하면 $v_i$들은 벡터공간 $\mathbb{F}^m$의 벡터이다. $S = \left\{1, 2, .., n \right\}$ ,  $\mathcal{I} = \left\{ I : I \subset S, \left\{v_i\right\}_{i \in I} \: are \: linearly \: independent \right\}$ 로 놓으면 $\mathcal{M} = (S, \mathcal{I})$는 matroid가 됨을 쉽게 알 수 있다. (1, 2번 조건은 자명하고, 3번의 경우 $|X| < |Y|$이고 둘 모두 independent한 vector들의 집합이므로 $X$의 벡터들이 $Y$의 벡터공간 전체를 span할 수 없다)

예시 2. Graphic matroid

$G = (V, E)$가 무향 그래프일 때,  $\mathcal{I} = \left\{I : I \subset E, I \: induces \: a \: forest \: in \: G \right\}$로 놓으면 $\mathcal{M} = (E, \mathcal{I})$는 matroid가 된다. 1, 2번 조건은 앞서와 마찬가지로 자명하고, 3번 조건의 경우 $X$에 포함된 edge들을 모두 이었을 때 component의 개수는 $N - |X|$이고, $X + y \in  \mathcal{I}$ 를 만족하는 $y \in Y \setminus X$가 존재하지 않는다면 $Y$의 edge들의 두 끝점이 한 component에 들어가야 하므로 $Y$에 포함된 edge들을 모두 이었을 때 component의 개수는 $N-|X|$ 이하인데 이것은 $N-|Y|$와 같아야 하므로 $|X| <|Y|$에 모순이다. 따라서, 3번 조건 역시 만족한다. Graphic matroid의 경우는 뒤에 다룰 minimum spanning tree를 구하는 kruskal 알고리즘의 증명에 이용된다.



예시 2-1. Graphic matroid의 변형

그래프에서 matroid는 예시 2처럼만 정의할 수 있는 것이 아니다. $G = (V, E)$가 무향 연결 그래프일 때, $\mathcal{I} = \left\{I : I \subset E, E - I \: connects \: all \: vertex \: in \: G \right\}$로 두면 $\mathcal{M} = (E, \mathcal{I})$는 matroid이다. $\mathcal{I}$가 공집합을 포함해야 하므로 $G$가 connected가 아닌 경우에는 matroid가 되지 않음에 주의해야 한다. 또 다른 예시로는 어떤 edge 집합으로 induced되는 그래프에서 각 component의 edge 개수가 vertex 개수를 넘지 않는 경우를 독립집합으로 정의하면 matroid가 된다. 두 가지 matroid 모두 정의 3이 간단히 증명되며, 나중에 소개할 maximum weight independent set algorithm을 이용하면 재미있는 결과를 얻을 수 있다.



예시 3. Uniform matroid

Uniform matroid는 어쩌면 생각할 수 있는 가장 쉬운 matroid이다. 어떠한 $k$를 정한 후 $S$에서 크기가 $k$ 이하인 모든 부분집합을 independent set으로 놓으면 uniform matroid가 된다.



예시 4. Partition matroid

Partition matroid는 Uniform matroid의 일반화라고 볼 수 있다. $S_1, S_2, ..., S_n$이 $S$의 분할이고, $k_1, k_2, ..., k_n$이 양의 정수일 때, $\mathcal{I} = \left\{ I : I \subset S, | I \cap S_i | \le k_i \: for \: all \: 1 \le i \le n \right\}$  로 정의하면 $\mathcal{M} = (S, \mathcal{I})$는 matroid이다. partition matroid나 uniform matroid 같은 경우는 matroid임이 자명하기 때문에 이것이 매트로이드라는 것이 특별한 것은 아니지만, 다음 포스팅에서 다룰 matroid intersection의 경우 graphic matroid나 vector matroid 등 다른 matroid와의 maximal matroid intersection / maximum weight matroid intersection을 구하는 문제 등에서 사용된다.



예시 5. Transversal matroid

$G = (V, E)$가 bipartition $V_1$과 $V_2 $를 가지는 이분그래프(bipartite graph)일 때, 

$\mathcal{I} = \left\{ I : I \subset V_1, \exist \: a \: matching \: M \: in \: G \: that \: covers \: I \right\}$ 로 두면 $\mathcal{M} = (V_1, \mathcal{I})$ 은 matroid이다. 3번 조건의 경우 $X$ 와 $Y$ 각각에 매칭된 vertex들을 생각하면 자명하다.



예시 6. Matching matroid

무향그래프 $G = (V, E)$에서 $\mathcal{I} = \left\{ I : I \subset V, \exist \: a \: matching \: M \: in \: G \: that \: covers \: I \right\}$ 로 두면 $\mathcal{M} = (V, \mathcal{I})$ 은 matroid이다.



##매트로이드에서 쓰이는 기본 용어 및 성질



정의 2. $\mathcal{M} = (S, \mathcal{I})$ 가 매트로이드일 때, $S$의 부분집합 중 $\mathcal{I}$에 포함되지 않는 것을 $\mathcal{M}$의  dependent set이라 한다.

정의 3. $\mathcal{M}$의 independent set $I$에 대해 $I$를 진부분집합으로 갖는 independent set이 없다면 $I$를 $\mathcal{M}$의 base라고 한다.

성질 1. $\mathcal{M}$의 모든 base들의 크기는 동일하다. 이것은 정의 3에 의해 간단히 증명할 수 있다.



정의 4. $\mathcal{M} = (S, \mathcal{I})$ 가 matroid이고 $S' \subset S$ 일 때, $\mathcal{I}' = \left\{ I : I \subset S', I \in \mathcal{I} \right\}$ 로 두면 $\mathcal{M}' = (S', \mathcal{I}') $ 역시 matroid이고 이를 $\mathcal{M}$의 $S'$에 대한 restriction이라고 한다. restriction이 matroid임은 정의에 의해 자명하다.



정의 5. matroid에서 minimal dependent set을 circuit이라 한다. 즉, $C \subset S$가 circuit일 조건은 $C \notin \mathcal{I}$이면서  $\forall x \in C, C-x \in \mathcal{I}$를 만족하는 경우이다. graphic matroid에서의 circuit은 matroid가 정의된 그래프에서 simple cycle을 이룬다. 

성질 2. $\mathcal{M} = (S, \mathcal{I})$ 가 matroid라 하자. $X \in \mathcal{I}, y \notin X$ 이면 $X+y \in \mathcal{I}$ 이거나 $X+y$가 unique한 circuit $C$를 포함하며, 그 경우 모든 $\widehat{y} \in C$ 에 대해 $X+y-\widehat{y} \in \mathcal{I}$ 가 성립한다.

증명. $X+y \notin \mathcal{I}$이면 $X + y$는 적어도 하나의 circuit을 포함한다. 이를 $C_1$이라 하자. 만약 $X + y$가 다른 circuit $C_2$도 포함한다면 $X$는 independent하기 때문에 $C_1$과 $C_2$는 모두 $y$를 포함한다. $C_1 + C_2 - y$를 생각하면 

#Maximum weight independent set in a matroid

matroid가 주어졌을 때, maximum weight independent set은 매우 빠른 시간에 계산할 수 있다. 또한, 음 아닌 정수 $k$가 주어졌을 때 size가 $k$인 independent set 중 weight가 maximum인 set도 쉽게 구할 수 있다. (minimum은 -1을 곱하면 maximum과 같은 방법으로 구해진다)

정리 1. 다음의 greedy 알고리즘은 $\mathcal{M} = (S, \mathcal{I})$의  maximum weight independent set을 올바르게 구한다.

1. $e \in S $의 weight을  $w(e)$로 표시하자. $e$가 loop(그 자체로 dependent한 원소)이거나 $w(e) \le 0$인 원소이면 무시한다.
2. 1에서 무시한 원소를 제거했을 때 $S = \left\{e_1, ..., e_n\right\}$ 에서 $w(e_1) \ge w(e_2) \ge ... \ge w(e_n)$ 이라 하자.
3. 초기 상태에서 $X \leftarrow \phi$.
4. $i$를 1부터 $n$까지 증가시키면서 $X + e_i$가 $\mathcal{I}$의 원소이면 $X \leftarrow X + e_i$를 대입한다.
5. $X$는 maximum weight independent set이다.

정리 1의 증명.

1번 step을 거치고 나면 $S = \left\{e_1, ..., e_n\right\}$ 에서 $w(e_1) \ge w(e_2) \ge ... \ge w(e_n) > 0$  이라 가정할 수 있다. 여기서 $e_1$을 포함하는 optimal solution(maximum weight independent set)이 항상 존재함을 보이면 $\mathcal{M}$의 $S-e_1$에 대한 restriction 역시 matroid이므로 수학적 귀납법에 의해 위의 greedy한 방법이 항상 optimal solution을 구한다는 것을 쉽게 보일 수 있다. 

$I^*$이  maximum weight independent set 중 하나라고 하자. $e_1 \in I^*$인 경우, claim을 만족하였다. $e_1 \notin I^*$인 경우 $I^*+e_1$은 dependent하므로 circuit을 가진다. 
