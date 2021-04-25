# Understanding the iterative version of Binary Exponentiation

![Photo by Erol Ahmed on Unsplash](https://cdn-images-1.medium.com/max/1000/1*M4N77KGez9Ulz9kHDSXaLA.jpeg)

Honestly, for me, understanding the recursive version of Binary Exponentiation was way easier than understanding its iterative version. And since you are here, I guess it might be the same for you. Anyway, let’s get straight to the point.

You may have noticed it already, as it’s pretty obvious.  
**Every decimal number can be expressed as the sum of some powers of 2.** For instance, 13 = 1 + 4 + 8 = 2⁰ + 2² + 2³; which indeed is how we convert any binary number to its decimal equivalent at the first place.   
Like, 1101\(binary\) = 2⁰ \* 1 + 2¹ \* 0 + 2² \* 1 + 2³ \* 1 = 2⁰ + 2² + 2³ = 13

Also, **every number N can be represented in ceil\(log₂N\) + 1 bits.**  
For instance, 8 = 1000\(binary\) i.e in 4 bits, 17 = 10001\(binary\) i.e in 5 bits and so on.

Keep the above two points in mind. They will be used soon.

Let's understand the following approaches with the example of calculating 3¹¹.

#### Naive approach

Calculates 3¹¹ as:   
We run a loop 11 times. Each time the result is multiplied by 3.  
3¹¹ = 3 . 3 . 3 . 3 . 3 . 3 . 3 . 3 . 3 . 3 . 3

So the loop run 11 times. Had the power been 10⁶, it would have run 10⁶ times. Thus its time complexity is O\(N\).

#### Binary Exponentiation approach

The naive approach looks at 3¹¹ as 3 . 3 . 3 . 3 . 3 . 3 . 3 . 3 . 3 . 3 . 3  
Whereas the binary exponentiation approach looks at 3¹¹ as 3¹. 3² . 3⁸;

**Where did we get this 1, 2, 8 power from?**  
Well, 11 = 1011₂ \(binary equivalent of 11\)   
1011₂ = 2⁰ + 2¹ + 2³ = 1 + 2 + 8

3¹¹ = 3¹⁺²⁺⁸ = 3¹. 3² . 3⁸

Our aim here is to calculate 3¹¹ in fewer steps, to be precise in ceil\(log₂11\) steps.

Let **a** be the base and **b** be the power.  
In the naive approach, with each iteration, we are multiplying the result with **a**, i.e by the same number every time. Can we do better?

Guess what, we can!  
After each iteration, we can replace **a** by **a²**. So in the case of 3¹¹, we will have 3¹¹ = 3¹ \* 3² \* 3⁴ …

Well, we have already discussed how 11 can be written as the sum of some powers of 2. Thus we know how 3¹¹ can be written as the product of 3 raised to some powers of 2.

Here’s the code —

```text
/* a is the base, b is the power. */
long long binpow(long long a, long long b) {     
   long long result = 1;
   while (b > 0) {
       /* 
       The below condition is true when b is odd, i.e when the
       leftmost bit of b is 1. Since with each iteration a is
       replaced by a², the set bit of b indicates that the current
       value of a is required to build up the result.
       */
       if (b % 2 == 1)
           result = result * a;
       /* 
       a maintains the value which needs to be multiplied when b
       becomes odd i.e when the last bit of b is 1.
       */
       a = a * a;
       /* 
       This is equivalent to right shift. 1011₂ first becomes  
       101₂, then 10₂, then 1₂, and at last 0₂. 
       */
       b /= 2;
   }
   return result;
}
```

I hope this makes sense.

Reference —

[**Powering Up With Binary Exponentiation**  
_Off-topic, this is quite the hectic time for me. Between course projects, passion projects, make-a-thons, online…_blogarithms.github.io](https://blogarithms.github.io/articles/2017-09/powering-up-with-binary-exponentiation)

[**Binary Exponentiation**  
_Binary exponentiation \(also known as exponentiation by squaring\) is a trick which allows to calculate $a^n$ using only…_cp-algorithms.com](https://cp-algorithms.com/algebra/binary-exp.html)

