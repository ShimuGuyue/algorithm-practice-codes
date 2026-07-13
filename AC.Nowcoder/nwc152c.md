

```cpp
void solve()
{
    int n;
    std::cin >> n;
    std::vector<std::pair<int, int>> edges(n);
    std::vector<int> degrees(n + 1);
    for (auto& [u, v] : edges)
    {
        std::cin >> u >> v;
        ++degrees[u];
        ++degrees[v];
    }

    int a, b;
    for (int i{ 1 }; i <= n; ++i)
    {
        if (degrees[i] == 1)
            a = i;
    }
    for (auto [u, v] : edges)
    {
        if (u == a || v == a)
        {
            std::cout << u << ' ' << v << '\n';
            return;
        }
    }
}
```

