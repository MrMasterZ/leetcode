### Code

    public boolean find132pattern(int[] nums) {
        int s3 = Integer.MIN_VALUE;
        Stack<Integer> st = new Stack<>();
        
        for(int i = nums.length - 1; i >= 0; i--) {
            if(nums[i] < s3) {                                  // поиск s1
                return true;
            } else {
                while(!st.isEmpty() && nums[i] > st.peek()) {
                    s3 = st.pop();
                }
                st.push(nums[i]);
            }
        }
        return false;
    }

### Explanation
1) поиск нашего pattern начинаем с конца
2) сначала найдём средний элемент (начально проинициализируем его самым минимальным int-значением)
3) этот средний элемент будет найден, если его из стека вытеснит какой-то элемент больше его
4) после того как его вытеснит элемент больше его нам останется найти только s1 (когда найдём такой s1, тогда return)
