#  Infix to Postfix Calculator (Stack-Based)

This is a stack-based calculator built with Python that converts and evaluates infix expressions by turning them into postfix (Reverse Polish Notation). It features a GUI made with `tkinter` and handles various operators with custom error handling.

---

## Features

- Supports multi-digit integers
- Handles parentheses
- Supports the following operators:
  - Arithmetic: `+`, `-`, `*`, `/`, `%`, `^`
  - Comparison: `<`, `>`, `<=`, `>=`, `==`, `!=`
  - Logical: `&&`, `||`, `!`
- Custom error messages (e.g., unclosed parentheses, divide by zero)
- Input length limit (256 characters)
- Clean and interactive GUI with `tkinter`

---

## Peek: Infix to Postfix Conversion

```python
def infix_to_postfix(expr):
    output, stack = [], []
    tokens = tokenize(expr)
    for token in tokens:
        if token.isdigit():
            output.append(token)
        elif token == '(':
            stack.append(token)
        elif token == ')':
            found_paren = False
            while stack:
                top = stack.pop()
                if top == '(':
                    found_paren = True
                    break
                output.append(top)
            if not found_paren:
                raise ValueError("unclosed parentheses")
        elif is_operator(token):
            while (stack and stack[-1] != '(' and
                   yes[token] <= yes.get(stack[-1], 0)):
                output.append(stack.pop())
            stack.append(token)
    while stack:
        if stack[-1] in '()':
            raise ValueError("unclosed parentheses")
        output.append(stack.pop())
    return output
