## Staircase problem
https://www.dailycodingproblem.com/blog/staircase-problem/

There exists a staircase with N steps, and you can climb up either 1 or 2 steps at a time.

Given N, write a function that returns the number of unique ways you can climb the staircase.
The order of the steps matters.

What if, instead of being able to climb 1 or 2 steps at a time, you could climb any number from a set of positive integers X? For example, if X = {1, 3, 5}, you could climb 1, 3, or 5 steps at a time.

#### My solution in JS
```javascript
function staircase(X, n) {
    return solution(X, n, [], 0)

    function solution(steps, n, result) {
        for (let i = 0; i < steps.length; i++) {
            let step = steps[i]
            if (n - step > 0) {
                result = solution(steps, n - step, result)
            } else if (n - step === 0) {
                return ++result
            } else if (n - step < 0)
                return
        }
        return result
    }
}
```
