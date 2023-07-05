# LC-Python31
Greedy Algorithm 6


## 738.Monotone Increasing Digits
July 04, 2023  4h

Congratulations!\
This is the 31th day for leetcode python study. Today we will learn about the Greedy Algorithm!\
The challenges today are especially about categorizing the situation into different parts clearly. Both questions today are by post-order loop/traversal. The first one is dealing with numbers, while the second one is accomplished with a binary search tree. A very good recap!


##  738.Monotone Increasing Digits
If two digits are not monotone increasing, we minus the i+1th digit to 1 and change the ith digit to 9. And we use a postorder loop from the last digit of the given number, so the beginning digits can use the updated results from the last digits.
```python 
class Solution:
    def monotoneIncreasingDigits(self, n: int) -> int:
        strNum = list(str(n))       #change the given integer to string for process

        for i in range(len(strNum)-1, 0, -1):       #post-order loop
            if strNum[i-1] > strNum[i]:     #not monotone increasing
                strNum[i-1] =  str(int(strNum[i-1]) - 1)
                strNum[i:] = '9' * (len(strNum) - i)
        
        return int(''.join(strNum))
```


## 968.Binary Tree Cameras
This is a combination of binary tree and greedy algorithm. Hard.\
We put a camera at each leaf nodes' father node, so the least number of cameras would be used. To accomplish this, we use post-order traversal, left-right-middle. We return the left and right kid nodes' situation to the father node.
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    #0: not covered
    #1: have camera here
    #2: covered by camera
    def minCameraCover(self, root: Optional[TreeNode]) -> int:
        result = [0]        #to record the number of cameras needed
        if self.traversal(root, result) == 0:   #if root is not covered
            result[0] += 1
        return result[0]

    def traversal(self, cur:TreeNode, result:List[int]) -> int:
        if not cur:     #reach a null node, then it is covered, so the father of leaf node can have camera, like situation 1.
            return 2
        
        left = self.traversal(cur.left, result)
        right = self.traversal(cur.right, result)

        if left == 2 and right == 2:
            return 0        #return 0 to the father node, means father node should be 0 not covered by camera
        if left == 0 or right == 0:
            result[0] += 1  #the result finally returned, number of camera needed increase by 1
            return 1        #return 1 to the father node, means father node should be 1 and have a camera here
        if left == 1 or right == 1:
            return 2        #return 2 to the father node, means father node should be covered by camera, but not need to place a camera here
```


## Summary




