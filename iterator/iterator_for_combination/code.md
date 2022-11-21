### Code

    class CombinationIterator { 
    private Stack<Integer> stack;
    private int len;
    private char[] chars;
    public CombinationIterator(String characters, int combinationLength) {
        len = combinationLength;
        chars = characters.toCharArray();
        stack = new Stack<>();
        for (int i = 0; i < combinationLength; i++) {
            stack.push(i);
        }
    }
    
    public String next() {
        if (!hasNext()) return "";
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < len; i++) {
            sb.append(chars[stack.get(i)]);
        }
        if (stack.peek() < len - 1) {
            stack.set(stack.size() - 1, stack.peek() + 1);
        } else {
            while (!stack.isEmpty() && stack.peek() >= chars.length - len + stack.size() - 1) {
                stack.pop();
            }
            if (!stack.isEmpty()) {
                stack.set(stack.size() - 1, stack.peek() + 1);
                int size = len - stack.size();
                for (int i = 0; i < size; i++) {
                    stack.push(stack.peek() + 1); 
                }
            }
         }
        
        return sb.toString();
    }
    
    public boolean hasNext() {
        return !stack.isEmpty();
    }
}
