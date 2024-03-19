# Hear me out
## Background
A medical devices company recently had to recall all of their latest hearing aids after they were reported to produce a loud popping sound if used near particular oscillators, such as Theragun and Waterpik\*. The new model of hearing aids offers an enhanced mode where noise due to the occlusion effect<sup>†</sup> is selectively filtered out by producing an inverted sound, effectively canceling noise inside the ear. However, there were circumstances when the outer microphones would pick up on the driver sounds, resulting in positive feedback. The medical devices company think they have a solution.

## Solution
Since the human frequency range is roughly 20 - 20,000 Hz, noise outside it is almost entirely inaudible. There are potentially unlimited producible frequencies above 20kHz given that the hearing aid tweeter capacity is 40kHz, so the solution is to embed a unique pattern that can be checked by the outer microphones for leakage. One option, which is the focus here, is to start with a square wave and decrease its amplitude until it is no longer detected by the outer mics. Modulating amplitude requires fractional multiplication, except the hardware only supports addition, subtraction, and shifting operators. While there are already functions to perform integer multiplication and division, they do not support mixed numbers. 

Here is their number class:
```python
class Number:
    def __init__(self, numerator, denominator=1):
        self.numerator = numerator
        self.denominator = denominator
    
    def __str__(self):
        return f'{self.numerator} / {self.denominator}'
    
    @staticmethod
    def integer_sum(a, b):
        assert a >= 0 and b >= 0
        _sum = 0
        carry = 0
        k = 1
        _a = a
        _b = b
        while _a or _b:
            ak = a & k
            bk = b & k
            _carry = (ak & bk) | (ak & carry) | (bk & carry)
            _sum |= ak ^ bk ^ carry
            carry = _carry << 1
            k <<= 1
            _a >>= 1
            _b >>= 1
        return _sum | carry
    
    @staticmethod
    def integer_product(a, b):
        _sum = 0
        while a:
            if a & 1:
                _sum = Number.integer_sum(_sum, b)
            a >>= 1
            b >>= 1
        return _sum
        
    @staticmethod
    def integer_quotient(a, b):
        diff = 0
        power = 32
        b_pow = b << power
        while a >= b:
            while b_pow > a:
                b_pow >>= 1
                power -= 1
            diff += 1 << power
            a -= b_pow
        return diff
    
    @staticmethod
    def gcd(a, b):
        if a > b:
            return Number.gcd(b, a)
        if a == 0:
            return b
        if not ((a & 1) or (b & 1)):
            return Number.gcd(a >> 1, b >> 1) << 1
        if not a & 1 and b & 1:
            return Number.gcd(a >> 1, b)
        if a & 1 and not b & 1:
            return Number.gcd(a, b >> 1)
        return Number.gcd(a, b - a)
    
    def product(self, other):
        numerator_prod = Number.integer_product(self.numerator, 
                                                other.numerator)
        denominator_prod = Number.integer_product(self.denominator, 
                                                  other.denominator)
        gcd = Number.gcd(numerator_prod, denominator_prod)
        return Number(
            Number.integer_quotient(numerator_prod, gcd), 
            Number.integer_quotient(denominator_prod, gcd))

    def quotient(self, other):
        return self.product(other.inverse())
    
    def inverse(self):
        return Number(self.denominator, self.numerator)
```

You can see that it already supports basic arithmetic for natural numbers. The issue herein pertains to rational numbers. 
## Expectations
* Identify the cause of divide by zero issues, or more broadly, issues with `Number::product` returning a 0 in the denominator, such as for 
```python
# prints 1/0 instead of 1/2, the simplified form of 6/12
print(Number(3,4).product(Number(2,3))) 
```
* Suggest a caching mechanism that would reduce runtime.

---
<font size=1>

\*This problem is inspired by an [issue with Apple's Airpods Pro](https://www.reddit.com/r/airpods/comments/yfmfuf/here_we_go_again_airpods_pro_2nd_gen_have_the/).
<sup>†</sup>The [occlusion effect](https://www.miracle-ear.com/blog-news/occlusion-effect) is when our own voice sounds strange after wearing something like earplugs or headphones because what's left is mostly transmission of vibrations through the skull.

</font>
