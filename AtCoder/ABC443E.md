

```c++
void solve()
{
    int n, m;
    std::cin >> n >> m;
    std::vector<std::string> grid(n + 1);
    for (int i = 1; i <= n; ++i)
    {
        std::string s;
        std::cin >> s;
        grid[i] = " " + s;
    }

    std::vector<std::vector<bool>> bools(n + 1, std::vector<bool>(n + 1));
    for (int j = 1; j <= n; ++j)
    {
        for (int i = n - 1; i >= 1; --i)
        {
            if (grid[i + 1][j] == '#')
                break;
            bools[i][j] = true;
        }
    }

    std::vector<std::vector<bool>> dp(n + 1, std::vector<bool>(n + 1));
    dp[n][m] = true;
    for (int i = n; i > 1; --i)
    {
        for (int j = 1; j <= n; ++j)
        {
            if (!dp[i][j])
                continue;
            for (int k : {j - 1, j, j + 1})
            {
                if (k < 1 || k > n)
                    continue;
                if (bools[i - 1][k])
                {
                    bools[i - 2][k] = true;
                    dp[i - 1][k] = true;
                }
                else
                {
                    if (grid[i - 1][k] == '.')
                        dp[i - 1][k] = true;
                }
            }
        }
    }
    for (int i = 1; i <= n; ++i)
    {
        std::cout << dp[1][i];
    }
    std::cout << '\n';
}
```

