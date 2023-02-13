## Sieve of Eratosthenes 


```python
def prime_list(n):
    # Updating a list with numbers from 0-n (assume all are prime)
    sieve = [True] * n

    # 
    m = int(n ** 0.5)
    for i in range(2, m + 1):
        if sieve[i] == True:           # i가 소수인 경우
            for j in range(i+i, n, i): # i이후 i의 배수들을 False 판정
                sieve[j] = False

    # 소수 목록 산출
    print(sieve)
    return [i for i in range(2, n) if sieve[i] == True]
    
print(prime_list(5))
```

    [True, True, True, True, False]
    [2, 3]
    

### Why is this necessary?
A generic code for determining whether a number is a prime number or not:


```python
def is_prime(n):
    if n > 1:
        for i in range(2, n):
            if n % i == 0:
                return False
        return True
    else:
        return False

print(is_prime(5))
```

    True
    

<br>In this case, the time complexity is O(n).</br>
<br>In reality we can solve the problem with O(n**0.5) time complexity.</br>
For instance with the number 8 the factors are symmetrical 2 * 4 = 4 * 2


```python
def is_prime(n):
    if n>1:
        for i in range(2, int(n**0.5)+1):
            if n % i == 0:
                return False
        return True
    else:
        return False
print(is_prime(97))
```

    True
    

<br>But what do we do if we want to check if multiple numbers are prime numbers?</br>
With the sieve, we first create an index in accordance with the range in which we are looking for prime numbers. (Hint: Easier to understand if we understand that the list starts from 0)
