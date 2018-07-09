
# Finite Field Multiplication and Exponentiation

Just as we defined a new addition ($+~f~$) for Finite Fields that was _closed_, we can also define a new multiplication for Finite Fields that's also closed. By multiplying the same number many times, we can also define exponentiation or power. In this section, we'll go through exactly how to define this using modulo arithmetic.

#### Solve these equations in \\(F_{31}\\):

\\(24\cdot19=?\\)

\\(17^3=?\\)

\\(5^5\cdot18=?\\)


```python
# remember that ** is the exponentiation operator
prime = 31
# 24*19=?
print(24*19 % prime)
# 17^3=?
print(17**3 % prime)
# 5^5*18=?
print(5**5*18 % prime)
```

#### Write a program to calculate \\(0k, 1k, 2k, 3k, ... 30k\\) for some k in \\(F_{31}\\).  Notice anything about these sets?


```python
from random import randint

prime = 31
k = randint(1,prime)

# use range(prime) to iterate over all numbers from 0 to 30 inclusive
print(sorted([i*k % prime for i in range(prime)]))
```

#### Write a program to calculate \\(k^{30}\\) for all k in \\(F_{31}\\). Notice anything?


```python
prime = 31

# use range(1, prime) to iterate over all numbers from 1 to 30 inclusive
print([i**30 % prime for i in range(1, prime)])
```

### Exercise

Create the `__mul__` and `__pow__` methods for your library:


```python
from ecc import FieldElement

class FieldElement(FieldElement):

    def __mul__(self, other):
        if self.prime != other.prime:
            raise RuntimeError('Primes must be the same')
        # self.num and other.num are the actual values
        num = (self.num * other.num) % self.prime
        # self.prime is what you'll need to mod against
        prime = self.prime
        # You need to return an element of the same class
        # use: self.__class__(num, prime)
        return self.__class__(num, prime)

    def __pow__(self, n):
        prime = self.prime
        num = pow(self.num, n, prime)
        # You need to return an element of the same class
        # use: self.__class__(num, prime)
        return self.__class__(num, prime)
```
