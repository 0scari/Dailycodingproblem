## Staircase problem
https://www.dailycodingproblem.com/blog/staircase-problem/

There exists a staircase with N steps, and you can climb up either 1 or 2 steps at a time.

Given N, write a function that returns the number of unique ways you can climb the staircase.
The order of the steps matters.

What if, instead of being able to climb 1 or 2 steps at a time, you could climb any number from a set of positive integers X? For example, if X = {1, 3, 5}, you could climb 1, 3, or 5 steps at a time.

#### My solution in JS
```javascript
function staircase(X, n) {
    return solution(X, n, 0)

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

## Array inversions

We can determine how "out of order" an array A is by counting the number of inversions it has. Two elements `A[i]` and `A[j]` form an inversion if `A[i]` > `A[j]` but `i` < `j`. That is, a smaller element appears after a larger element.

Given an array, count the number of inversions it has. Do this faster than O(N^2) time.

You may assume each element in the array is distinct.

#### My solution in JS
```javascript
// The solution uses unbalanced binary search tree.
// If it were explicitly stated the input array could be modified,
// a better option would've been in-place Insertion Sort.

let test1 = [2, 4, 1, 3, 5]  // res: 3
let test2 = [5, 4, 3, 2, 1]  // res: 10

function countInversions(list) {
   let tree = new InversionCountingTree()
   for (var i = list.length - 1; i >= 0; i--) {
      tree.insertAndCount(list[i])
   }
   return tree.inversionCount
}

class InversionCountingTree {
   constructor() {
      this.inversionCount = 0
   }

   insertAndCount(newValue) {
      if (this.root) {
         this.inversionCount += this._insertAndCountRec(this.root, newValue, 0)
      } else {
         this.root = new Node(newValue)
      }
   }

   _insertAndCountRec(node, newValue, inversionCount) {
      node.childNodeCount++
      if (newValue > node.value) {
         if (inversionCount === 0) inversionCount = node.childNodeCount
         insert(node.greaterNode)
      } else {
         insert(node.lesserNode)
      }
      return inversionCount

      function insert(nextNode) {
         // code broke for test1 after introducing this function
         if (nextNode) {
            return this._insertAndCountRec(node, newValue, inversionCount)
         } else {
            nextNode = new Node(newValue)
         }
      }
   }
}

class Node {
   constructor(value) {
      this.value = value
      this.lesserNode
      this.greaterNode
      this.childNodeCount = 0
   }
}

```
