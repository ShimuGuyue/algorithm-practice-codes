

```
class Solution
{
public:
    vector<int> twoSum(vector<int>& nums, int target)
    {
        map<int, vector<int>> indexs;
        for (int i{ 0 }; i < nums.size(); ++i)
        {
            indexs[nums[i]].push_back(i);
        }

        for (int i{ 0 }; i < nums.size(); ++i)
        {
            if (nums[i] * 2 == target)
            {
                if (indexs[nums[i]].size() > 1)
                    return { indexs[target - nums[i]][0], indexs[target - nums[i]][1] };
            }
            else if (indexs.count(target - nums[i]))
                return { i, indexs[target - nums[i]][0] };
        }
        return {};
    }
};
```
