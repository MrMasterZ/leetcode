### Code №1 (fastest)

    public int[] smallerNumbersThanCurrent(int[] nums) {
        int res[] = new int[nums.length];
        int numberArray[] = new int[101];  // у нас иапазон от 0 до 100

        for (int i = 0; i < nums.length; i++) {   // считаем сколько раз данное число из nums употребляется в nums
            numberArray[nums[i]]++;
        }

        for (int i = 1; i < numberArray.length; i++) {  // сумммирует (накапливает) число вхождений из этой ячейки и из предыдущей
            numberArray[i] = numberArray[i] + numberArray[i-1];
        }

        for (int i = 0; i < nums.length; i++) {
            res[i] = (nums[i] == 0) ? 0:numberArray[nums[i] - 1];  // 0 -- минимальное число в нашей задаче, если у нас не 0, то берём кол-во из предыдущей ячейки nums
        }

        return res;
    }

### Notice №1
* Это самый быстрый алгоритм O(N), но требует дополнительной памяти для хранения значений из numberArray. А если у нас диапазон допустимых значений будет значительно больше?

### Code №2

    public int[] smallerNumbersThanCurrent(int[] nums) {
      int[] ans = new int[nums.length];
        for(int i = 0; i < nums.length; i++) {
            int count = 0;
            for (int k : nums) {
                if (nums[i] > k) {
                    count++;
                }
            }
            ans[i] = count;
        }
        return ans;
    }

### Notice №2
* Временная сложность этого алгоритма O(N^2), но он не требует содавать дополнительную структуру данных для хранения количества значений из диапазона (numberArray)
