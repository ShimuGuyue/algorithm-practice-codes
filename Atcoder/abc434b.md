

```c++
void solve()
{
    int n, m;
    std::cin >> n >> m;
    std::vector<std::vector<int>> birds(m + 1);
    while (n--)
    {
        int a, b;
        std::cin >> a >> b;
        birds[a].push_back(b);
    }

    for (int i = 1; i <= m; ++i)
    {
        int sum = std::accumulate(birds[i].begin(), birds[i].end(), 0);
        double ans = 1.0 * sum / birds[i].size();
        std::cout << std::fixed << std::setprecision(10) << ans << '\n';
    }
}
```

