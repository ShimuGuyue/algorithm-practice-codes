

```c++
void solve()
{
    int n;
    std::cin >> n;
    std::vector<int> as(n + 1);
    for (int i = 1; i <= n; ++i)
    {
        std::cin >> as[i];
    }

    std::vector<int> turns(n + 1);
    for (int i = 1; i <= n; ++i)
    {
        if (as[i])
            turns[i] = i;
        else
            turns[i] = turns[i - 1];
    }

    std::vector<int> dp(n + 1);
    std::vector<int> presums_dp(n + 1);
    presums_dp[0] = dp[0] = 1;
    for (int i = 1; i <= n; ++i)
    {
        int flag{ 0 };
        int j{ i };
        while (j > 0 && (flag & as[j]) == 0)
        {
            flag |= as[j];
            j = turns[j - 1];
        }
        if (j == 0)
            dp[i] = presums_dp[i - 1];
        else
            dp[i] = (presums_dp[i - 1] - presums_dp[j - 1] + mod) % mod;
        presums_dp[i] = (presums_dp[i - 1] + dp[i]) % mod;
    }
    std::cout << dp[n] << '\n';
}
```

