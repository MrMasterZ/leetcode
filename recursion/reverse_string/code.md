### Code №1 (simplest)

    public void reverseString(char[] s) {
           for (int p1 = 0, p2 = s.length - 1; p1 < p2; p1++, p2--) {
            char temp = s[p1];
            s[p1] = s[p2];
            s[p2] = temp;
        }
    }

### Code №2 (with recursion)

    public void reverseString(char[] s) {
        giveMeReversedString(s, 0, s.length-1);
    }
    
    private static void giveMeReversedString(char[] s, int start, int end) {
        if (start >= end)
            return;
        
        char temp = s[start];
        s[start] = s[end];
        s[end] = temp;
        
        giveMeReversedString(s, ++start, --end);
    }
