

```cpp
void solve()
{
    int n;
    std::cin >> n;
    std::vector<int64_t> as(n + 1);
    std::vector<int64_t> bs(n + 1);
    for (int i{ 1 }; i <= n; ++i)
    {
        std::cin >> as[i];
    }
    for (int i{ 1 }; i <= n; ++i)
    {
        std::cin >> bs[i];
    }

    std::vector<std::vector<int64_t>> dp(n + 1, std::vector<int64_t>(2));
    for (int i{ 1 }; i <= n; ++i)
    {
        int64_t a{ as[i] };
        int64_t b{ bs[i] };
        if (a <= 0)
        {
            dp[i][0] = dp[i][1] = std::max(dp[i - 1][0], dp[i - 1][1]);
            continue;
        }
        if (b & 1)
        {
            dp[i][0] = std::max(dp[i - 1][0], dp[i - 1][1]) + b / 2 * a;
            dp[i][1] = std::max(dp[i - 1][0] + (b / 2 + 1) * a, dp[i - 1][1] + b / 2 * a);
        }
        else
        {
            dp[i][0] = std::max(dp[i - 1][0] + b / 2 * a, dp[i - 1][1] + (b / 2 - 1) * a);
            dp[i][1] = std::max(dp[i - 1][0], dp[i - 1][1] + b / 2 * a);
        }
    }

    int64_t ans{ std::max(dp[n][0], dp[n][1]) };
    std::cout << ans << '\n';
}
```

