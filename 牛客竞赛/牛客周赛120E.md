

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

    std::vector<bool> isleave(n + 1);
    for (int i = 2; i <= n; ++i)
    {
        if (tree[i].size() == 1)
            isleave[i] = true;
    }

    std::vector<std::pair<int, int>> ans(n + 1); // <h, cnt>
    for (int i = 1; i <= n; ++i)
    {
        if (!isleave[i])
            continue;
        ans[i] = {0, 0};
        int next = tree[i].front();
        ans[next] = {1, 1};
    }

    auto dfs = [&tree, &ans, &isleave](auto &&dfs, int u, int last)
    {
        if (isleave[u])
            return;
        for (int v : tree[u])
        {
            if (v == last)
                continue;
            dfs(dfs, v, u);
            if (ans[v].first + 1 > ans[u].first)
            {
                ans[u].first = ans[v].first + 1;
                ans[u].second = ans[v].second;
            }
            else if (ans[v].first + 1 == ans[u].first)
            {
                ans[u].second += ans[v].second;
            }
        }
    };
    dfs(dfs, 1, 0);

    for (int i = 1; i <= n; ++i)
    {
        std::cout << ans[i].second << ' ';
    }
    std::cout << '\n';
}
```

