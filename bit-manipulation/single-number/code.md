### Code

    class Solution {
      public int singleNumber(int[] nums) {
          int result = 0;
          for(int i = 0;i<nums.length;i++){
            result = result ^ nums[i];
          }
       return result;
       }
    }

### Explanation
Такое поведение следует из свойств XOR (двоичный оператор) : 1) x ^ 0 = x    2) x ^ x = 0     3) 3) x ^ y = y ^ x  (позволяет менять местами)  
Если у нас есть последовательность операций XOR a ^ b ^ c ^ ..., то из неё можно убрать все пары повторяющихся значений, и это не повлияет на результат.
