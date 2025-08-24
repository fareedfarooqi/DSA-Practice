# 1700. Number of Students Unable to Eat Lunch (Easy)

---

## 🔗 LeetCode Link

Here is the link to the problem on LeetCode:  
[**Number of Students Unable to Eat Lunch**](https://leetcode.com/problems/number-of-students-unable-to-eat-lunch/description/)

---

## Problem Description

The school cafeteria offers **circular** and **square** sandwiches at lunch break, represented by:

- `0`: Circular sandwiches
- `1`: Square sandwiches

### Rules:

1. Students stand in a **queue** and can either:
   - Take the sandwich at the top of the stack if it matches their preference.
   - Move to the end of the queue if it doesn't match.
2. This process continues until:
   - A student eats their preferred sandwich.
   - None of the students in the queue want the sandwich at the top of the stack.
3. The task is to return the number of students who are **unable to eat**.

### Inputs:

- `students`: An integer array where `students[i]` represents the sandwich preference of the i-th student in the queue.
- `sandwiches`: An integer array where `sandwiches[i]` represents the type of sandwich at the i-th position in the stack (`i = 0` is the top of the stack).

### Output:

Return the number of students who are unable to eat.

---

## Examples

### Example 1:

**Input**:
`students = [1, 1, 0, 0]`
`sandwiches = [0, 1, 0, 1]`

**Output**:
`0`

**Explanation**:

- Initial: `students = [1, 1, 0, 0]`, `sandwiches = [0, 1, 0, 1]`

1. Front student prefers 1, top sandwich is 0 → student moves to the back → students = [1, 0, 0, 1].
2. Repeat: students = [0, 0, 1, 1].
3. Front student prefers 0, takes the top sandwich → students = [0, 1, 1], sandwiches = [1, 0, 1].
4. Process continues until all sandwiches are eaten and no students remain.
   Result: All students ate.

## Approach & Algorithm

- I have utilised a queue data structure to solve this problem.
- I am treating the students array as a queue.
- When the number associated with the first element in `students` equals to the first element in `sandwiches` the student prefers that sandwich and thus they are both removed from their respective arrays.
- When the student at the front of `students` array does not prefer the sandwich at the front of `sandwiches` array i.e., their elements **don't** match then, we simply pop the student from the front of the array and append them to the end. This way we cycle through all the students in the `students` array to see if they can have the sandwich at the top of the stack.
- We also have a `count` variable. This variable keeps track of how many consecutive students cannot have the sandwich at the top of the `sandwiches` stack i.e., how many students from `students` array do not have a matching element to the front element of the `sandwiches` array.

## Code Solutions

### Solution One - Treating 'Students' as a Queue

- **Time Complexity**: It is `O(n^2)`.

```python
class Solution:
    def countStudents(self, students: List[int], sandwiches: List[int]) -> int:
        student = None
        count = 0

        while students:
            if students[0] == sandwiches[0]:
                students.pop(0)
                sandwiches.pop(0)
                count = 0

            else:
                student = students.pop(0)
                students.append(student)
                count += 1

            # Meaning no student can have the sandwich on the top of the stack
            if count == len(students):
                break

        return len(students)
```

### Solution Two - Deque

```python
from collections import deque

class Solution:
    def countStudents(self, students: List[int], sandwiches: List[int]) -> int:
        # Convert the students to a queue.
        studentsQueue = deque(students)
        sandwichesQueue = deque(sandwiches)
        print(f"{studentsQueue} -- {sandwichesQueue}")

        while True:
            # Compare the top level values.
            if len(studentsQueue) == 0 or len(sandwichesQueue) == 0:
                return 0

            if studentsQueue[0] == sandwichesQueue[0]:
                studentsQueue.popleft()
                sandwichesQueue.popleft()
            else:
                # Implies student does not like this particular sandwich.
                setOfStudents = set(studentsQueue)

                if len(setOfStudents) == 1:
                    return len(studentsQueue)
                
                # Otherwise we carry on.
                studentThatDidNotLikeSandwich = studentsQueue.popleft()
                studentsQueue.append(studentThatDidNotLikeSandwich)
        
        return len(studentsQueue)
```
