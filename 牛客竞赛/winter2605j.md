

```c++
void solve()
{
    std::array<std::array<int, 3>, 3> grid;
    for (auto& v : grid)
    {
        for (auto& a : v)
        {
            std::cin >> a;
        }
    }

    int sum{ grid[0][0] + grid[0][1] + grid[0][2] };
    if (grid[1][0] + grid[1][1] + grid[1][2] != sum)
    {
        std::cout << "No\n";
        return;
    }
    if (grid[2][0] + grid[2][1] + grid[2][2] != sum)
    {
        std::cout << "No\n";
        return;
    }
    if (grid[0][0] + grid[1][0] + grid[2][0] != sum)
    {
        std::cout << "No\n";
        return;
    }
    if (grid[0][1] + grid[1][1] + grid[2][1] != sum)
    {
        std::cout << "No\n";
        return;
    }
    if (grid[0][2] + grid[1][2] + grid[2][2] != sum)
    {
        std::cout << "No\n";
        return;
    }
    if (grid[0][0] + grid[1][1] + grid[2][2] != sum)
    {
        std::cout << "No\n";
        return;
    }
    if (grid[0][2] + grid[1][1] + grid[2][0] != sum)
    {
        std::cout << "No\n";
        return;
    }
    std::set<int> t;
    for (auto& v : grid)
    {
        for (auto a : v)
        {
            t.insert(a);
        }
    }
    if (t.size() != 9)
    {
        std::cout << "No\n";
        return;
    }
    std::cout << "Yes\n";
}
```

