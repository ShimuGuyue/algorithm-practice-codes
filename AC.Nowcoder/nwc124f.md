

```c++
void solve()
{
    int n;
    std::cin >> n;
    std::string s;
    std::cin >> s;
    s = " " + s + s;
    std::vector<int64_t> as(n * 2 + 1);
    for (int i = 1; i <= n; ++i)
    {
        std::cin >> as[i];
        as[i + n] = as[i];
    }


    std::vector<std::vector<int64_t>> dp(n * 2 + 1, std::vector<int64_t>(n * 2 + 1, 1e18));
    for (int i = 2; i <= n * 2; ++i)
    {
        if (s[i - 1] == s[i])
        {
            dp[i - 1][i] = as[i - 1] * as[i];
        }
    }
    for (int len = 4; len <= n; len += 2)
    {
        for (int l = 1; l + len - 1 <= n; ++l)
        {
            int r = l + len - 1;
            if (s[l] == s[r])
                dp[l][r] = std::min(dp[l][r], dp[l + 1][r - 1] + as[l] * as[r]);
            for (int k = l + 1; k < r; k += 2)
            {
                dp[l][r] = std::min(dp[l][r], dp[l][k] + dp[k + 1][r]);
            }
        }
    }

    int64_t ans{ int64_t(1e18) };
    for (int i = 1; i <= n; ++i)
    {
        ans = std::min(ans, dp[i][i + n - 1]);
    }
    if (ans == 1e18)
        ans = -1;
    std::cout << ans << '\n';
}
```

