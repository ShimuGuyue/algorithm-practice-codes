

```c++
void solve()
{
    int n, m, k;
    std::cin >> n >> m >> k;
    std::vector<std::vector<int>> grid(n + 1, std::vector<int>(m + 1));
    for (int i = 1; i <= n; ++i)
    {
        for (int j = 1; j <= m; ++j)
        {
            std::cin >> grid[i][j];
        }
    }

    std::vector<int> counts(n + 1);
    while (k--)
    {
        int b;
        std::cin >> b;
        for (int i = 1; i <= n; ++i)
        {
            counts[i] += std::count(grid[i].begin(), grid[i].end(), b);
        }
    }
    int ans{ *std::max_element(counts.begin() + 1, counts.end()) };
    std::cout << ans << '\n';
}
```

