# 1472. Design Browser History (Medium)

## Problem Description

You have a browser with one tab where you start on the homepage, and you can:

1. Visit another URL.
2. Move back in the history by a certain number of steps.
3. Move forward in the history by a certain number of steps.

Implement the `BrowserHistory` class:

- `BrowserHistory(string homepage)`: Initializes the object with the homepage of the browser.
- `void visit(string url)`: Visits `url` from the current page. Clears all the forward history.
- `string back(int steps)`: Moves `steps` back in history. If `steps > x` (where `x` is the number of previous pages), it moves back only `x` steps. Returns the current URL after moving back.
- `string forward(int steps)`: Moves `steps` forward in history. If `steps > x` (where `x` is the number of forward pages), it moves forward only `x` steps. Returns the current URL after moving forward.

---

## Examples

### Example 1:

**Input**:
["BrowserHistory","visit","visit","visit","back","back","forward","visit","forward","back","back"]
[["leetcode.com"],["google.com"],["facebook.com"],["youtube.com"],[1],[1],[1],["linkedin.com"],[2],[2],[7]]

**Output**:

# 1472. Design Browser History

## Problem Description

You have a browser with one tab where you start on the homepage, and you can:

1. Visit another URL.
2. Move back in the history by a certain number of steps.
3. Move forward in the history by a certain number of steps.

Implement the `BrowserHistory` class:

- `BrowserHistory(string homepage)`: Initializes the object with the homepage of the browser.
- `void visit(string url)`: Visits `url` from the current page. Clears all the forward history.
- `string back(int steps)`: Moves `steps` back in history. If `steps > x` (where `x` is the number of previous pages), it moves back only `x` steps. Returns the current URL after moving back.
- `string forward(int steps)`: Moves `steps` forward in history. If `steps > x` (where `x` is the number of forward pages), it moves forward only `x` steps. Returns the current URL after moving forward.

---

## Examples

### Example 1:

**Input**:
["BrowserHistory","visit","visit","visit","back","back","forward","visit","forward","back","back"]
[["leetcode.com"],["google.com"],["facebook.com"],["youtube.com"],[1],[1],[1],["linkedin.com"],[2],[2],[7]]

**Explanation**:
BrowserHistory browserHistory = new BrowserHistory("leetcode.com");
browserHistory.visit("google.com"); // You are in "leetcode.com". Visit "google.com".
browserHistory.visit("facebook.com"); // You are in "google.com". Visit "facebook.com".
browserHistory.visit("youtube.com"); // You are in "facebook.com". Visit "youtube.com".
browserHistory.back(1); // Move back to "facebook.com". Returns "facebook.com".
browserHistory.back(1); // Move back to "google.com". Returns "google.com".
browserHistory.forward(1); // Move forward to "facebook.com". Returns "facebook.com".
browserHistory.visit("linkedin.com"); // Visit "linkedin.com" and clear forward history.
browserHistory.forward(2); // Cannot move forward any steps. Returns "linkedin.com".
browserHistory.back(2); // Move back to "facebook.com", then to "google.com". Returns "google.com".
browserHistory.back(7); // Move back to the homepage "leetcode.com". Returns "leetcode.com".

## Approach & Algorithm

### Doubly Linked-List

- Upon first glance, this problem appeared to be a problem that can be solved using a doubly linked list.
- I created a smaller `WebsiteNode` class which keeps track of the individual website itself. It has `website_name`, `prev` (keeps track of previous websites), and a `next` (to keep track of next websites in the browsers history) variables.
- I then used these `WebsiteNode` to create the websites and inserted them into the `BrowserHistory`.
- I've utilised a `cur_ptr` to keep track of where we are currently in the browser history, i.e., we can have 3 websites in our browser history: `google.com`, `youtube.com` and `facebook.com`. If we are currently viewing `youtube.com` our `cur_ptr` will point to `youtube.com`, even though we have `facebook.com` ahead of `youtube.com` in the browser history.

## Code Solutions

### Solution 1: Insertion Method (Not Fast)

- **Time Complexity**: It is `O(1)`.

```python
class BrowserHistory:

    def __init__(self, homepage: str):
        self.homepage = WebsiteNode(homepage)
        self.cur_ptr = self.homepage

    def visit(self, url: str) -> None:
        # Visiting a website is simply adding a new node (remove forward nodes)
        new_website = WebsiteNode(url, self.cur_ptr, None)
        self.cur_ptr.next = new_website
        self.cur_ptr = new_website
        return

    def back(self, steps: int) -> str:
        current = self.cur_ptr
        step_count = 0

        while current.prev is not None:
            if step_count == steps:
                self.cur_ptr = current
                return current.website_name

            current = current.prev
            step_count += 1

        self.cur_ptr = current
        return current.website_name


    def forward(self, steps: int) -> str:
        # Move forward in the linked list
        current = self.cur_ptr
        step_count = 0

        while current.next is not None:
            if step_count == steps:
                self.cur_ptr = current
                return current.website_name

            current = current.next
            step_count += 1

        self.cur_ptr = current
        return current.website_name

class WebsiteNode:
    def __init__(self, website_name="", prev=None, next=None):
        self.website_name = website_name
        self.prev = prev
        self.next = next

# Your BrowserHistory object will be instantiated and called as such:
# obj = BrowserHistory(homepage)
# obj.visit(url)
# param_2 = obj.back(steps)
# param_3 = obj.forward(steps)
```
