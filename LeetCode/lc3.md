

```cpp
class Solution
{
public:
    int lengthOfLongestSubstring(string )
    {
        if (.length() == 0)
            return 0;

        vector<int> counts(128);
        int ans{ 1 };
        int l{ 0 }, r{ 0 };
        while (r < .length())
        {
            ++counts[[r]];
            while (counts[[r]] > 1)
            {
                --counts[[l]];
                ++l;
            }
            ans = std::max(ans, r - l + 1);
            ++r;
        }
        return ans;
    }
};
```
