

```c++
void solve()
{
    int n;
    std::cin >> n;
    std::vector<std::vector<int>> tree(n + 1);
    for (int i = 1; i < n; ++i)
    {
        int u, v;
        std::cin >> u >> v;
        tree[u].push_back(v);
        tree[v].push_back(u);
    }

    int ans{ 0 };
    auto dfs = [n, &tree, &ans](auto&& dfs, int u, int last) -> int
    {
        bool ok{ true };
        int sum{ 0 };
        for (int v : tree[u])
        {
            if (v == last)
                continue;
            int count{ dfs(dfs, v, u) };
            if (count % 2 == 0)
                ok = false;
            sum += count;
        }
        if (sum + 1 != n && (n - sum - 1) % 2 == 0)
            ok = false;
        if (ok)
            ++ans;
        return sum + 1;
    };
    dfs(dfs, 1, 0);
    std::cout << ans << '\n';
}
```

