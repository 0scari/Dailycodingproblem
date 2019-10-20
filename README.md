## Staircase problem
https://www.dailycodingproblem.com/blog/staircase-problem/

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
