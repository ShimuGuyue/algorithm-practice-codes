

```c++

static constexpr int lcm{ 56 };
void solve()
{
    int64_t n, a, b;
    std::cin >> n >> a >> b;

    int64_t count{ n / lcm };
    if (count)
        --count;
    int64_t sum{ count * lcm };
    int64_t last{ n - sum };

    int64_t ans{ std::max({sum / 8 * (a + b), sum / 7 * a, sum / 2 * b}) };
    std::vector<int64_t> dp(last + 1);
    for (int i{ 0 }; i <= last; ++i)
    {
        if (i >= 2)
            dp[i] = std::max(dp[i], dp[i - 2] + b);
        if (i >= 7)
            dp[i] = std::max(dp[i], dp[i - 7] + a);
        if (i >= 8)
            dp[i] = std::max(dp[i], dp[i - 8] + a + b);
    }
    ans += dp[last];
    std::cout << ans << '\n';
}
```

