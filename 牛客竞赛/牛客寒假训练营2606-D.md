

```c++
void solve()
{
    using loc = std::array<int, 3>;

    int n, m, a, b;
    std::cin >> n >> m >> a >> b;
    std::vector<std::vector<int>> grid(n + 1, std::vector<int>(m + 1));
    std::priority_queue<loc, std::vector<loc>, std::greater<loc>> h;
    while (a--)
    {
        int x, y;
        std::cin >> x >> y;
        h.push({0, x, y});
        grid[x][y] = 1;
    }
    std::map<std::pair<int, int>, int> times;
    while (b--)
    {
        int x, y, t;
        std::cin >> x >> y >> t;
        grid[x][y] = 2;
        times[{x, y}] = t;
    }
    int ans{ 0 };
    while (!h.empty())
    {
        auto [t, x, y]{ h.top() };
        h.pop();
        ans = std::max(ans, t);

        static constexpr std::array<std::array<int, 2>, 4> dxy{{
            {-1, 0}, {0, -1}, {0, 1}, {1, 0}
        }};
        for (auto [dx, dy] : dxy)
        {
            int xx{ x + dx };
            int yy{ y + dy };
            if (xx < 1 || xx > n )
                continue;
            if (yy < 1 || yy > m)
                continue;
            if (grid[xx][yy] == 1)
                continue;
            if (grid[xx][yy] == 0)
                h.push({t + 1, xx, yy});
            else
                h.push({std::max(times[{xx, yy}], t + 1), xx, yy});
            grid[xx][yy] = 1;
        }
    }
    std::cout << ans << '\n';
}
```

