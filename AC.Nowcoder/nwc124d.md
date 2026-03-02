

```c++
void solve()
{
    int n;
    std::cin >> n;
    std::vector<int> counts(n + 1);
    for (int i = 1; i < n; ++i)
    {
        int u, v;
        std::cin >> u >> v;
        ++counts[u];
        ++counts[v];
    }

    int count = std::count_if(counts.begin() + 1, counts.end(),
        [](int x)
        {
            return x < 2;
        }
    );

    int ans{ (count + 1) / 2 };
    std::cout << ans << '\n';
}
```

