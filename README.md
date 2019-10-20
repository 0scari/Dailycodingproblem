## Staircase problem
https://www.dailycodingproblem.com/blog/staircase-problem/

There exists a staircase with N steps, and you can climb up either 1 or 2 steps at a time.

Given N, write a function that returns the number of unique ways you can climb the staircase.
The order of the steps matters.

#### My solution in JS
```javascript
function staircase(X, n) {
    return solution(X, n, [], 0)

    function solution(stepNumbers, remainingSteps, acc, result) {
        for (let i = 0; i < stepNumbers.length; i++) {
            let step = stepNumbers[i]
            if (remainingSteps - step > 0) {
                acc.push(step)
                result = solution(stepNumbers, remainingSteps - step, acc, result)
            } else if (remainingSteps - step === 0) {
                acc.push(step)
                result += 1
                acc.pop()
                return result
            } else if (remainingSteps - step < 0)
                return
            acc.pop()
        }
        return result
    }
}
```
