

```c++
void solve()
{
    int n;
    std::cin >> n;
    std::vector<std::vector<int>> grid(n, std::vector<int>(n));
    std::vector<std::vector<int>> visited(n, std::vector<int>(n));

    std::queue<std::array<int, 3>> q;
    q.push({0, 0, n % 2 == 0 ? 1 : 0});
    while (!q.empty())
    {
        auto [x, y, v]{ q.front() };
        q.pop();

        grid[x][y] = v;

        if (x + 1 != n && !visited[x + 1][y])
        {
            visited[x + 1][y] = true;
            q.push({x + 1, y, (v + 1) % 2});
        }
        if (y + 1 != n && !visited[x][y + 1])
        {
            visited[x][y + 1] = true;
            q.push({x, y + 1, (v + 1) % 2});
        }
        if (x + 1 != n && y + 1 != n && !visited[x + 1][y + 1])
        {
            visited[x + 1][y + 1] = true;
            q.push({x + 1, y + 1, (v + 1) % 2});
        }
    }

    for (auto& v : grid)
    {
        for (auto a : v)
        {
            std::cout << a;
        }
        std::cout << '\n';
    }
}
```

