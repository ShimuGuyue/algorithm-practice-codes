

```cpp
void solve()
{
    std::string s;
    std::cin >> s;

    int n{ int(s.length()) };
    s = " " + s;

    int max{ 0 };
    int count;
    std::vector<int> dp(n + 1);
    for (int i{ 1 }; i <= n; ++i)
    {
        if (s[i] == '(')
            continue;
        if (s[i - 1] == '(')
        {
            dp[i] = dp[i - 2] + 2;
        }
        else
        {
            if (s[i - 1 - dp[i - 1]] == '(')
            {
                dp[i] = dp[i - 1] + 2;
                dp[i] += dp[i - dp[i]];
            }
        }
        if (dp[i] > max)
        {
            max = dp[i];
            count = 1;
        }
        else if (dp[i] == max)
        {
            ++count;
        }
    }
    if (max == 0)
        count = 1;
    std::cout << max << ' ' << count << '\n';
}
```

