### 筛法求质数

---

#### 朴素筛法 - O(nlogn)

算法：从2~n枚举，对于每个数我们把它的所有倍数都筛掉，这样剩下未被筛掉的数就是质数。

缺点：把每个数的倍数都筛了一遍，有很多重复筛选

```c++
int primes[N];// 质数列表
bool st[N];// 是否筛掉
void get_prime(int n){
  int cnt = 0;
  for(int i = 2; i <= n; i++) {
    // 没有被筛掉 则为质数
    if(!st[i]) primes[cnt++] = i;
    // 把i的所有倍数筛掉
    for(int j = 2; i * j <= n; j++) {
      st[i * j] = true;
    }
  }
}
```

#### 埃氏筛法 - O(nloglogn)

算法：从2~n枚举，对于每个质数我们把它的所有倍数都筛掉，这样剩下未被筛掉的数就是质数。

改进：针对朴素筛法，不需要对每个数都筛掉它的倍数，只需要筛掉质数的倍数，因为所有合数都是由质数组成的

缺点：不同质数的倍数有可能是同一个数，还是有重复筛选

```c++
int primes[N];// 质数列表
bool st[N];// 是否筛掉
void get_prime(int n){
  int cnt = 0;
  for(int i = 2; i <= n; i++) {
    // 没有被筛掉 则为质数
    if(!st[i]) {
      primes[cnt++] = i;
      // 把i的所有倍数筛掉
      for(int j = 2; i * j <= n; j++) {
        st[i * j] = true;
      }
    }
  }
}
```

#### 线性筛法 - O(n)

算法：从2~n枚举，对每一个数都从之前的质数中去找它的最小质因子，找到了就break掉，这样剩下未被筛掉的数就是质数。

改进：由于质因子都是成对出现的，因此同样我们只需要枚举较小的那个质因子即可（即所有合数都只会被它的最小质因子筛掉）

```c++
int primes[N];// 质数列表
bool st[N];// 是否筛掉
void get_prime(int n){
  int cnt = 0;
  for(int i = 2; i <= n; i++) {
    // 没有被筛掉 则为质数
    if(!st[i]) primes[cnt++] = i;
    //把已筛出来的质数的i倍筛掉
    for(int j = 0; primes[j] <= n/i; j++) {
      st[primes[j] * i] = true;
      //找到i的最小质因子，加上这个优化就会变为线性的
      if(i % primes[j] == 0) break;
    }
  }
}
```

