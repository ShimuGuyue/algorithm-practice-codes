

```cpp
void solve()
{
    int n, x, y;
    std::cin >> n >> x >> y;
    std::vector<std::pair<int, int>> abs(n + 1);
    abs[0] = {x, y};
    for (int i{ 1 }; i <= n; ++i)
    {
        std::cin >> abs[i].first >> abs[i].second;
    }

    std::vector<int> indegrees(n + 1);
    std::vector<std::vector<bool>> graph(n + 1, std::vector<bool>(n + 1));
    for (int i{ 0 }; i <= n; ++i)
    {
        auto [a1, b1]{ abs[i] };
        for (int j{ 1 }; j <= n; ++j)
        {
            auto [a2, b2]{ abs[j] };
            if (a1 < a2 && b1 < b2)
            {
                ++indegrees[j];
                graph[i][j] = true;
            }
        }
    }

    std::queue<int> q;
    for (int i{ 1 }; i <= n; ++i)
    {
        if (indegrees[i] == 0)
            q.push(i);
    }
    while (!q.empty())
    {
        int u{ q.front() };
        q.pop();
        for (int v{ 1 }; v <= n; ++v)
        {
            if (!graph[u][v])
                continue;
            --indegrees[v];
            if (indegrees[v] == 0)
                q.push(v);
        }
    }

    std::vector<int> lens(n + 1);
    std::vector<int> lasts(n + 1);
    q.push(0);
    while (!q.empty())
    {
        int u{ q.front() };
        q.pop();
        for (int v{ 1 }; v <= n; ++v)
        {
            if (!graph[u][v])
                continue;
            if (lens[u] + 1 > lens[v])
            {
                lens[v] = lens[u] + 1;
                lasts[v] = u;
            }
            --indegrees[v];
            if (indegrees[v] == 0)
                q.push(v);
        }
    }

    int max{ 0 };
    int index;
    for (int i{ 1 }; i <= n; ++i)
    {
        if (lens[i] > max)
        {
            max = lens[i];
            index = i;
        }
    }
    std::cout << max << '\n';
    if (max == 0)
        return;
    std::vector<int> path;
    while (index)
    {
        path.push_back(index);
        index = lasts[index];
    }
    std::reverse(path.begin(), path.end());
    for (auto a : path)
    {
        std::cout << a << ' ';
    }
    std::cout << '\n';
}
```

