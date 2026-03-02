

```c++
void solve()
{
    int n;
    std::cin >> n;
    std::vector<std::vector<bool>> grid(n + 2, std::vector<bool>(n + 2));
    for (int i = 1; i <= n; ++i)
    {
        std::string s;
        std::cin >> s;
        for (int j = 0; j < n; ++j)
        {
            if (s[j] == '1')
                grid[i][j + 1] = 1;
        }
    }

    std::vector<std::vector<bool>> visited(n + 2, std::vector<bool>(n + 2));
    std::queue<std::pair<int, int>> q;
    for (int i = 1; i <= n; ++i)
    {
        for (int j = 1; j <= n; ++j)
        {
            if (!grid[i][j])
                continue;
            if (grid[i - 1][j - 1])
            {
                if (!visited[i][j - 1])
                {
                    visited[i][j - 1] = true;
                    q.push({i, j - 1});
                }
                if (!visited[i - 1][j])
                {
                    visited[i - 1][j] = true;
                    q.push({i - 1, j});
                }
            }
            if (grid[i - 1][j + 1])
            {
                if (!visited[i - 1][j])
                {
                    visited[i - 1][j] = true;
                    q.push({i - 1, j});
                }
                if (!visited[i][j + 1])
                {
                    visited[i][j + 1] = true;
                    q.push({i, j + 1});
                }
            }
            if (grid[i + 1][j + 1])
            {
                if (!visited[i][j + 1])
                {
                    visited[i][j + 1] = true;
                    q.push({i, j + 1});
                }
                if (!visited[i + 1][j])
                {
                    visited[i + 1][j] = true;
                    q.push({i + 1, j});
                }
            }
            if (grid[i + 1][j - 1])
            {
                if (!visited[i + 1][j])
                {
                    visited[i + 1][j] = true;
                    q.push({i + 1, j});
                }
                if (!visited[i][j - 1])
                {
                    visited[i][j - 1] = true;
                    q.push({i, j - 1});
                }
            }
        }
    }
    while (!q.empty())
    {
        auto [x, y]{ q.front() };
        q.pop();

        grid[x][y] = true;
        if (grid[x - 1][y - 1])
        {
            if (!visited[x][y - 1])
            {
                visited[x][y - 1] = true;
                q.push({x, y - 1});
            }
            if (!visited[x - 1][y])
            {
                visited[x - 1][y] = true;
                q.push({x - 1, y});
            }
        }
        if (grid[x - 1][y + 1])
        {
            if (!visited[x - 1][y])
            {
                visited[x - 1][y] = true;
                q.push({x - 1, y});
            }
            if (!visited[x][y + 1])
            {
                visited[x][y + 1] = true;
                q.push({x, y + 1});
            }
        }
        if (grid[x + 1][y + 1])
        {
            if (!visited[x][y + 1])
            {
                visited[x][y + 1] = true;
                q.push({x, y + 1});
            }
            if (!visited[x + 1][y])
            {
                visited[x + 1][y] = true;
                q.push({x + 1, y});
            }
        }
        if (grid[x + 1][y - 1])
        {
            if (!visited[x + 1][y])
            {
                visited[x + 1][y] = true;
                q.push({x + 1, y});
            }
            if (!visited[x][y - 1])
            {
                visited[x][y - 1] = true;
                q.push({x, y - 1});
            }
        }
    }

    for (int i = 1; i <= n; ++i)
    {
        for (int j = 1; j <= n; ++j)
        {
            std::cout << (grid[i][j] ? 1 : 0);
        }
        std::cout << '\n';
    }
}
```

