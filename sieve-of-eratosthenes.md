# Sieve Of Eratosthenes

Sieve of Eratosthenes is an algorithm for finding all prime numbers in any given range. Here are the topics that I have tried to cover in this article.

### Topics discussed in this article <a id="a635"></a>

* What are prime numbers?
* Naive way of finding prime numbers.
* Sieve of Eratosthenes \(sounds more like a king’s name! **No Offence intended.**\)
* Segmented Sieve
* Finding prime number in a particular range

So if you are interested in any of these topics, then perhaps this article is for you.

## What are prime numbers? <a id="5f64"></a>

> _No doubt, Every number is beautiful.  
> But Prime number’s beauty just cannot go unnoticed!_

The Prime numbers are those positive Natural numbers which cannot be properly divided by any positive Natural number less than it\(except 1\).

So 2, 3, 5, 7 are prime numbers. But 4, 6, 8, 9, 10 are not.

## Naive way of finding Prime number <a id="8898"></a>

The most obvious way to find whether a number is prime or not, is perhaps to :

* Run a loop from 2 to n-1\(n being the number to be checked\)
* Check if there is any number that can properly divide n. If you find one, then it is not a prime number, else it is.

This process can be further optimized by just running the loop from 2 to square root of n.

**Thinking why square root of n?**  
Well here’s why we do that thing:  
If x \* y = N  
then we can also write  
x \* y = N = √_N \*_ √_N_  
If _x_ ≤ √N, then _y_ ≥ √N and vice-versa. Thus if x divides N, then you just don’t have to check if y also divides it, because it does.

## Sieve of Eratosthenes <a id="b4d7"></a>

The above discussed way worked just fine. But imagine finding all prime numbers up to N. In that case you will have to repeat above discussed approach for every number less than N. So time complexity will be **O\(N√N\)**.  
That’s when **Sieve of Eratosthenes** comes into picture. It’s time complexity is _O_\(_n_ log log _n_\).

I have a cool analogy.

Imagine two kingdoms. One ruled by _King A_ and other by _King B._ Prosperity and happiness were spread all around. But then, a deadly infectious disease started spreading in both kingdoms. Where once was happiness and prosperity, now death and disease danced their way around. Both the kings handled the situation differently.  
King A, being a bit carefree in nature, hospitalized the sufferer when they themselves came for check up. In this way, he was able to treat the one who was suffering, but didn’t care about other potential spreaders. Thus the disease kept spreading and the kingdom was destroyed.

Whereas King B, being more intelligent and far sighted, not only treated the one who was suffering, but also tracked all those people who could be potential spreader and hospitalized them. In this way, he prevents disease from spreading and saves his people’s lives.  
_**Long live the King B!**_

So our Sieve of Eratosthenes is like King B.

In this algorithm,

* Once we are sure a number is prime\(which second point will tell how\), _**We cross off all it’s multiple in the range.**_ Thus saving us time by not checking again if those multiples are prime when we are sure they aren’t\(because they already are divisible by our newly found prime number, so how can they be prime?\).
* Also another thing that can be easily concluded is, Starting from the beginning, if we find that the number has so far not been _crossed off_, then it just won’t be anytime in the future\(because there is no one\(except 1\) that can divide it properly\)! Hence is prime.



![](https://miro.medium.com/max/1750/0*auO27notXYgAZXUP.gif)

![Source: Internet](https://miro.medium.com/freeze/max/60/0*auO27notXYgAZXUP.gif?q=20)

The above figure makes it more clear.  
We first encounter 2 which has so far not been crossed off\(1 cannot cancel others, else no one will survive\). So we can safely infer that 2 is prime.  
All the multiples of 2 are then crossed off\(You can surely see them in red above\).

After all 2’s multiple are crossed away, we move ahead and stop at next _non-crossed off_ number, 3 in this case. So 3 is also prime because it has survived so far. We again _cross off_ all 3’s multiple. And then head on to next _non-crossed_ soul.  
And we keep one doing this till we cannot find any other prime number.

This is Sieve of Eratosthenes.

```text
// Implementation of Sieve of Eratosthenes
int n;
vector<bool> is_prime(n+1, true); 
is_prime[0] = is_prime[1] = false; 
for (int i = 2; i * i <= n; i++) { 
  if (is_prime[i]) { 
    for (int j = i * i; j <= n; j += i) 
      is_prime[j] = false; 
  } 
}
```

## Segmented Sieve <a id="1232"></a>

Sieve of Eratosthenes algorithm is nice. But there are times when it might not work.  
Eg. When n is pretty big, like around 10⁹, the array of size 10⁹ might not fit in the memory. Thus forming the array is\_prime of size 10⁹ is not possible, therefore we need to modify it.

The modification that segmented sieve offers is:  
As the name suggests, we have something to do with segments. Here instead of sieving out all prime numbers from complete heap at once, we are going to sieve them out from smaller heaps i.e from a small _**segment**_ of heap. Thus in this way, we can overcome the problem related to the maximum size of array possible.

Steps used in segmented sieve:

* Using simple sieve algorithm, find all primes up to √N \( which then will be used to cancel all composite numbers \).
* Now we are going to divide the given range in certain block size S\(at most √N\).
* And then for each block, we are going to map the values to their indexes. How? Well, each block will be like \[low, … , high\]. We will have array of size high-low+1. low will be mapped to index 0, \(low + 1\) to index 1, \(low + k\) to index k and so on…

```text
void print_all_primes(int n) { 
  const int S = 10000;           // block size
  vector<int> primes; 
  int nsqrt = sqrt(n);
            
  // Simple Sieve for finding prime numbers up to sqrt n
  vector<bool> is_prime(nsqrt + 1, true); 
  for (int i = 2; i <= nsqrt; i++) { 
    if (is_prime[i]) { 
      primes.push_back(i); 
      for (int j = i * i; j <= nsqrt; j += i) 
        is_prime[j] = false; 
      } 
  } 
 
  vector<bool> block(S); 
  for (int k = 0; k * S <= n; k++) { 
    fill(block.begin(), block.end(), true); 
    int start = k * S;           // starting value of the range of block
    int j;
    for (int p : primes) {      
      // Here we will find out the first index whose element is 
      // divisible by p(p being the element from prime array).
      int rem = start % p;
      if(rem == 0)
        j = rem;
      else 
        j = p - rem;
      for (; j < S; j += p){
        if(j == p - start) continue;       // because we don't want to 
                                           // mark the prime as not prime. 
        block[j] = false;
      }
     } 
    if (k == 0) 
      block[0] = block[1] = false; 
    for (int i = 0; i < S && start + i <= n; i++) { 
      if (block[i]) 
       cout << start + i << " ";          // start+i is the value at ith 
                                          // index of the block array. 
    } 
  } 
  cout << "\n";
}
```

This program helps in finding prime number when n is large enough and thus we are not able to store in an array at once.

## Finding prime number in a particular range <a id="a360"></a>

With segmented sieve at our disposal, finding prime number in a particular range is pretty simple.  
Actually we have already done it. In segmented sieve, we have divided our big range in some blocks of fixed sizes. And then printed prime numbers from all those blocks one by one.  
Now we are just provided with one random block. All we have to do is, Print prime numbers from that block.  
Try doing it yourself!

For any help, see how I solved a [similar problem.](https://github.com/palak001/CP-solutions/blob/master/spoj/2.PRIME1.cpp)  


