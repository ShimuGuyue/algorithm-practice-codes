

```c++
void solve()
{
    int n, m;
    std::cin >> n >> m;
    std::vector<std::map<int, int>> grid(n + 1);
    while (m--)
    {
        int u, v, w;
        std::cin >> u >> v >> w;
        if (u == v)
            continue;
        if (grid[u].find(v) == grid[u].end())
            grid[u][v] = w;
        else
            grid[u][v] = std::min(grid[u][v], w);
        if (grid[v].find(u) == grid[v].end())
            grid[v][u] = w;
        else
            grid[v][u] = std::min(grid[v][u], w);
    }

    std::vector<int64_t> min_lens(n + 1, std::numeric_limits<int64_t>::max());
    std::vector<int> last_nodes(n + 1);
    std::vector<bool> visited(n + 1);

    using pair = std::pair<int64_t, int>;
    std::priority_queue<pair, std::vector<pair>, std::greater<pair>> h;
    h.push({0, 1});
    while (!h.empty())
    {
        auto [len, u]{ h.top() };
        h.pop();

        if (visited[u])
            continue;
        visited[u] = true;

        for (auto [v, w] : grid[u])
        {
            if (visited[v])
                continue;
            if (len + w < min_lens[v])
            {
                min_lens[v] = len + w;
                last_nodes[v] = u;
                h.push({min_lens[v], v});
            }
        }
    }

    if (min_lens[n] == std::numeric_limits<int64_t>::max())
    {
        std::cout << -1 << '\n';
        return;
    }

    std::vector<int> ans;
    int node{ n };
    while (node != 0)
    {
        ans.push_back(node);
        node = last_nodes[node];
    }
    std::reverse(ans.begin(), ans.end());
    for (auto a : ans)
    {
        std::cout << a << ' ';
    }
    std::cout << '\n';
}
```

