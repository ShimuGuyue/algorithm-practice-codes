

```cpp
void solve()
{
    int n;
    std::cin >> n;
    std::vector<std::vector<int>> as(n + 1);
    for (int i{ 1 }; i <= n; ++i)
    {
        int m;
        std::cin >> m;
        as[i].resize(m + 1);
        for (int j{ 1 }; j <= m; ++j)
        {
            std::cin >> as[i][j];
        }
    }
    int x, y;
    std::cin >> x >> y;
    std::cout << as[x][y] << '\n';
}
```

