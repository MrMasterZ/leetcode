### Code

    class Solution {
    public int search(int[] nums, int target) {
        int maxIndex = nums.length - 1;
        int minIndex = 0;
        while(maxIndex != minIndex) {
            int index = minIndex + (maxIndex-minIndex)/2;
            if (target == nums[index])
                return index;
            else if (target < nums[index])
                maxIndex = index;
            else minIndex = index + 1;
        }
        if(target == nums[maxIndex])
            return maxIndex;
        else return -1;
    }
}
