

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

    std::vector<int64_t> dp(n + 1);
    int flag{ 0 }, count{ 0 };
    for (int i = 1; i <= n; ++i)
    {
        if (flag != as[i])
        {
            flag = as[i];
            count = 0;
        }
        ++count;
        if (count >= as[i])
            dp[i] = 1;
    }

    int64_t ans{};
    for (int i = 1; i <= n; ++i)
    {
        if (dp[i] == 0)
            continue;
        dp[i] += dp[i - as[i]];
        ans += dp[i];
    }
    std::cout << ans << '\n';
}
```

