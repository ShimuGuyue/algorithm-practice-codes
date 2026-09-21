

```c++
void solve()
{
    std::array<std::array<int, 4>, 4> grid;
    for (auto& v : grid)
    {
        for (auto& a : v)
        {
            std::cin >> a;
        }
    }

    for (int i = 0; i < 4; ++i)
    {
        std::set<int> t;
        for (int j = 0; j < 4; ++j)
        {
            t.insert(grid[i][j]);
        }
        if (t.size() != 4)
        {
            std::cout << "NO\n";
            return;
        }
    }

    for (int j = 0; j < 4; ++j)
    {
        std::set<int> t;
        for (int i = 0; i < 4; ++i)
        {
            t.insert(grid[i][j]);
        }
        if (t.size() != 4)
        {
            std::cout << "NO\n";
            return;
        }
    }

    {
        std::set<int> t;
        t.insert(grid[0][0]);
        t.insert(grid[0][1]);
        t.insert(grid[1][0]);
        t.insert(grid[1][1]);
        if (t.size() != 4)
        {
            debug_(0);
            std::cout << "NO\n";
            return;
        }
    }
    {
        std::set<int> t;
        t.insert(grid[0][2]);
        t.insert(grid[0][3]);
        t.insert(grid[1][2]);
        t.insert(grid[1][3]);
        if (t.size() != 4)
        {
            debug_(1);
            std::cout << "NO\n";
            return;
        }
    }
    {
        std::set<int> t;
        t.insert(grid[2][0]);
        t.insert(grid[2][1]);
        t.insert(grid[3][0]);
        t.insert(grid[3][1]);
        if (t.size() != 4)
        {
            debug_(2);
            std::cout << "NO\n";
            return;
        }
    }
    {
        std::set<int> t;
        t.insert(grid[2][2]);
        t.insert(grid[2][3]);
        t.insert(grid[3][2]);
        t.insert(grid[3][3]);
        if (t.size() != 4)
        {
            debug_(3);
            std::cout << "NO\n";
            return;
        }
    }

    std::cout << "YES\n";
}
```

