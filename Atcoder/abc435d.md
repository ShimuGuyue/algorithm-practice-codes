

```c++
void solve()
{
    int n, m;
    std::cin >> n >> m;
    std::vector<std::vector<int>> grid(n + 1);
    for (int i = 0; i < m; ++i)
    {
        int x, y;
        std::cin >> x >> y;
        grid[y].push_back(x);
    }

    std::vector<bool> gotoblack(n + 1);

    int q;
    std::cin >> q;
    while (q--)
    {
        int op, v;
        std::cin >> op >> v;
        if (op == 1)
        {
            std::queue<int> q;
            q.push(v);
            while (!q.empty())
            {
                int x{ q.front() };
                q.pop();
                if (gotoblack[x])
                    continue;
                gotoblack[x] = true;
                for (int y : grid[x])
                {
                    q.push(y);
                }
            }
        }
        else
        {
            std::cout << (gotoblack[v] ? "Yes" : "No") << '\n';
        }
    }
}
```

