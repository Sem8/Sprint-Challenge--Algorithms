Add your answers to the Algorithms exercises here.

## Exercise I

Give an analysis of the running time of each snippet of
pseudocode with respect to the input size n of each of the following:

```
a)  a = 0                       O(1)
    while (a < n * n * n):      O(n^3)
      a = a + n * n             O(1)
```
Answer a: O(n^3)
Answer a explanation: Since the while loops and for loops increase linearly as number of inputs increase, their time complexity is O(n). And we have 3 inputs (n) being multiplied to each other so their time complexity is O(n^3). When we assign variables, their time complexity is usually constant time of O(c) or in this case O(1) because it remains constant no matter how big n gets. We multiply whatever time complexity is inside the for or while loops with the time complexity of the loop so 'O(1) * O(n^3) = O(n^3)'. And the time complexity of whatever code is at the same level gets added together so, O(1) + O(n^3) = O(1 + n^3) which is the precise way to put it. But since only the highest value matters because when n gets very large like 1 million, the lower values won't affect time much, the highest values will take over and affect time the most. So, O(1 + n^3) gets reduced to O(n^3)

```
b)  sum = 0                                     O(1)           
    for i in range(n):                          O(n)
      i += 1                                    O(1)
      for j in range(i + 1, n):                 O(n)
        j += 1                                  O(1)
        for k in range(j + 1, n):               O(n)
          k += 1                                O(1)
          for l in range(k + 1, 10 + k):        O(k)    
            l += 1                              O(1)       
            sum += 1                            O(1)
```
Answer b: O(kn^3) can be reduced to O(n^3)
Answer b explanation: A for loop increases linearly so, its time complexity is O(n). Time complexity of any code inside a loop gets multiplied by the time complexity of that parent loop. Time complexity of code at the same indentation level gets added togther. Since we have 3 for loops inside a for loop it seems it should be O(n*n*n*n*n) so O(4^n) but since the 4th loop increases by order O(k) and not n it is O(k*n^3). To be more exact and precise, going from outside in, we have O(1) + O(n) * O(1) + O(n) = O(n^2 + n) + O(1) in the first for loop. In second loop, we have O(n^2 + n) * (O(1) + O(n)) = O(n^2 + n + n^3 + n^2) when we multiply time complexity results from first, second and third loop which comes down to now O(n^3 + 2n^2 + n). And for the final loop, the fourth loop, we have k so it is O(n^3 + 2n^2 + n) * (O(k) + O(1) + O(1)) which comes down to O(kn^3 + 2kn^2 + kn) + O(2n^3 + 4n^2 + 2n). And when n gets to be very large, only the largest value will dominate so the time complexity here can be reduced to O(kn^3) or just O(n^3).

```
c)  def bunnyEars(bunnies):
      if bunnies == 0:                      O(1)
        return 0                            O(1)

      return 2 + bunnyEars(bunnies-1)       O(n)    
```
Answer c: O(n)
Answer c explanation: O(n) because there's a recursive call and recursive calls increase by order of n depending on how many recursive calls there are. The other variables above the recursive call equate to O(1) so it is actually (O(1) * O(1)) + O(n) which equates to O(1 + n) but again since the highest value dominates when n gets very large like a million, we will only consider the highest value which is n so time complexity is O(n).

## Exercise II

Suppose that you have an _n_-story building and plenty of eggs. Suppose also that an egg gets broken if it is thrown off floor _f_ or higher, and doesn't get broken if dropped off a floor less than floor _f_. Devise a strategy to determine the value of _f_ such that the number of dropped eggs is minimized.

Write out your proposed algorithm in plain English or pseudocode and give the runtime complexity of your solution.

Answer: To try and reduce the number of eggs dropped we can mimic the binary search approach here. Determine the halfway point of the total number of floors. For example, if we have 10 floors, in this case it will 5. If you have an even number of floors and there is no exact halfway point and you want to err on the side of caution, we can choose so start with floor 6 and start with dropping an egg from there. If the egg breaks from floor 6, we can again cut the lower half of floors 1 to 6 by half again, so floor 3 would be the halfway point here. Then drop the egg from floor 3 and see if it breaks. Alternatively, if egg does not break from floor 6, we can take the upper half, floors 7-10 and cut that in half and drop the egg from that midway point so, to err on the side of caution, we can drop the egg from floor 9. If egg breaks from floor 9 but not floor 6, we again cut the lenght between 9 and 6 in half and err on the side of caution and drop from floor 8. If it breaks we move on to floor 7 because that's the only floor left after cutting our floor lengths in half. If it doesn't break from floor 8 we just spent 3 eggs determining the egg's break point instead of supposed 8 eggs if we were to test 1 floor at a time. We can follow the exact same way, from the bottom half of 6th floor if the egg did break from the 6th floor, cutting length in half from floors 1-6, if egg breaks cut the lower half and find the midpoint again and so on. Since we reduced the egg break from 8 to 3, we can say the time complexity is O(logn) because we're reducing the number of operations by half at each run and log(8) with base 2 = 3 or 2^3 = 8. 