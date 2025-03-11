# Skill_lab_code
#include <stdio.h>
#include <limits.h>

// Stack structure to hold the stack elements
struct Stack {
    int arr[100];
    int top;
};

// Initialize stack
void initStack(struct Stack* stack) {
    stack->top = -1;
}

// Push operation with O(1) support for getMin
void push(struct Stack* stack, int val) {
    if (stack->top == -1) {
        stack->arr[++stack->top] = val;  // If the stack is empty, push the element.
    } else {
        if (val < stack->arr[stack->top]) {
            // If the new value is smaller than the current minimum, store the difference
            stack->arr[++stack->top] = 2 * val - stack->arr[stack->top];
        } else {
            // Otherwise, just push the element
            stack->arr[++stack->top] = val;
        }
    }
}

// Pop operation
int pop(struct Stack* stack) {
    if (stack->top == -1) {
        printf("Stack is empty\n");
        return -1;
    }
    int topValue = stack->arr[stack->top--];
    
  // If the top value is less than the current minimum, we need to restore the old minimum
  if (topValue < stack->arr[stack->top + 1]) {
        int originalMin = stack->arr[stack->top + 1];
        stack->arr[stack->top + 1] = 2 * originalMin - topValue;
    }
        return topValue;
}

// Get the current minimum element in O(1) time
int getMin(struct Stack* stack) {
    if (stack->top == -1) {
        printf("Stack is empty\n");
        return -1;
    }
    return stack->arr[stack->top] < stack->arr[stack->top + 1] ? stack->arr[stack->top] : stack->arr[stack->top + 1];
}

// Main function to test the stack
int main() {
    struct Stack stack;
    initStack(&stack);

  push(&stack, 10);
    push(&stack, 5);
    push(&stack, 15);
    push(&stack, 2);
  printf("Current Minimum: %d\n", getMin(&stack));
    pop(&stack);
    printf("Current Minimum after pop: %d\n", getMin(&stack));
    return 0;
}
