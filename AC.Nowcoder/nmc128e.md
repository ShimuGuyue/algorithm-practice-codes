

```c++
void solve()
{
    int n, m, k;
    std::cin >> n >> m >> k;

    // 上限
    {
        int count{ ((n + 2) / 3) * ((m + 2) / 3) };
        if (k > n * m - count)
        {
            std::cout << -1 << '\n';
            return;
        }
    }

    std::vector<std::vector<int>> grid(n, std::vector<int>(m, 1));
    for (int i = 0; i < n; ++i)
    {
        if (k == 0)
            break;
        for (int j = 0; j < m; ++j)
        {
            if (k == 0)
                break;
            bool b1{ false }, b2{ false };
            if (i % 3 == 1 || (n % 3 == 1 && i == n - 1))
                b1 = true;
            if (j % 3 == 1 || (m % 3 == 1 && j == m - 1))
                b2 = true;
            if (b1 && b2)
                continue;
            grid[i][j] = 0;
            --k;
        }
    }
    for (auto& v : grid)
    {
        for (auto a : v)
        {
            std::cout << a;
        }
        std::cout << '\n';
    }
}
```

