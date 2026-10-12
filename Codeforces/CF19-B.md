

```cpp
void solve()
{
    int n;
    std::cin >> n;
    std::vector<int> ts(n + 1);
    std::vector<int64_t> cs(n + 1);
    for (int i{ 1 }; i <= n; ++i)
    {
        std::cin >> ts[i] >> cs[i];
    }

    std::vector<int> vs(n + 1);
    for (int i{ 1 }; i <= n; ++i)
    {
        vs[i] = ts[i] + 1;
    }

    int m{ 2001 + n };
    std::vector<std::vector<int64_t>> dp(n + 1, std::vector<int64_t>(m + 1, INT64_C(1) << 60));
    dp[0][0] = 0;
    for (int i{ 1 }; i <= n; ++i)
    {
        for (int j{ 0 }; j <= m; ++j)
        {
            dp[i][j] = dp[i - 1][j];
            if (j >= vs[i])
                dp[i][j] = std::min(dp[i][j], dp[i - 1][j - vs[i]] + cs[i]);
        }
    }
    int64_t ans{ INT64_C(1) << 60 };
    for (int i{ n }; i <= m; ++i)
    {
        ans = std::min(ans, dp[n][i]);
    }
    std::cout << ans << '\n';
}
```

