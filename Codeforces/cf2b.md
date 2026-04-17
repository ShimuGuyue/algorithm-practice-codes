

```cpp
void solve()
{
    int n;
    std::cin >> n;
    std::vector<std::vector<int>> grid(n + 1, std::vector<int>(n + 1));
    for (int i{ 1 }; i <= n; ++i)
    {
        for (int j{ 1 }; j <= n; ++j)
        {
            std::cin >> grid[i][j];
        }
    }

    auto calc2 = [](int n) -> int
    {
        if (n == 0)
            return 1;
        int ans{ 0 };
        while (n % 2 == 0)
        {
            n /= 2;
            ++ans;
        }
        return ans;
    };
    auto calc5 = [](int n) -> int
    {
        if (n == 0)
            return 1;
        int ans{ 0 };
        while (n % 5 == 0)
        {
            n /= 5;
            ++ans;
        }
        return ans;
    };

    std::vector<std::vector<int>> dp2(n + 1, std::vector<int>(n + 1, n * n));
    std::vector<std::vector<char>> path2(n + 1, std::vector<char>(n + 1));
    dp2[1][1] = calc2(grid[1][1]);
    for (int i{ 1 }; i <= n; ++i)
    {
        for (int j{ 1 }; j <= n; ++j)
        {
            int c{ calc2(grid[i][j]) };
            if (i != 1)
            {
                if (dp2[i - 1][j] + c < dp2[i][j])
                {
                    dp2[i][j] = dp2[i - 1][j] + c;
                    path2[i][j] = 'D';
                }
            }
            if (j != 1)
            {
                if (dp2[i][j - 1] + c < dp2[i][j])
                {
                    dp2[i][j] = dp2[i][j - 1] + c;
                    path2[i][j] = 'R';
                }
            }
        }
    }

    std::vector<std::vector<int>> dp5(n + 1, std::vector<int>(n + 1, n * n));
    std::vector<std::vector<char>> path5(n + 1, std::vector<char>(n + 1));
    dp5[1][1] = calc5(grid[1][1]);
    for (int i{ 1 }; i <= n; ++i)
    {
        for (int j{ 1 }; j <= n; ++j)
        {
            int c{ calc5(grid[i][j]) };
            if (i != 1)
            {
                if (dp5[i - 1][j] + c < dp5[i][j])
                {
                    dp5[i][j] = dp5[i - 1][j] + c;
                    path5[i][j] = 'D';
                }
            }
            if (j != 1)
            {
                if (dp5[i][j - 1] + c < dp5[i][j])
                {
                    dp5[i][j] = dp5[i][j - 1] + c;
                    path5[i][j] = 'R';
                }
            }
        }
    }

    bool find0{ false };
    int x, y;
    for (int i{ 1 }; i <= n; ++i)
    {
        for (int j{ 1 }; j <= n; ++j)
        {
            if (grid[i][j] == 0)
            {
                find0 = true;
                x = i,
                y = j;
            }
        }
    }

    int ans{ std::min(dp2[n][n], dp5[n][n]) };
    if (ans > 1 && find0)
    {
        std::cout << 1 << '\n';
        int i{ 1 }, j{ 1 };
        while (i < x)
        {
            std::cout << 'D';
            ++i;
        }
        while (j < y)
        {
            std::cout << 'R';
            ++j;
        }
        while (i < n)
        {
            std::cout << 'D';
            ++i;
        }
        while (j < n)
        {
            std::cout << 'R';
            ++j;
        }
        return;
    }
    std::cout << ans << '\n';
    std::vector<char> path;
    x = n; y = n;
    if (dp2[n][n] == ans)
    {
        while (x != 1 || y != 1)
        {
            path.push_back(path2[x][y]);
            if (path2[x][y] == 'D')
                --x;
            else
                --y;
        }
    }
    else
    {
        while (x != 1 || y != 1)
        {
            path.push_back(path5[x][y]);
            if (path5[x][y] == 'D')
                --x;
            else
                --y;
        }
    }
    std::reverse(path.begin(), path.end());
    for (auto c : path)
    {
        std::cout << c;
    }
    std::cout << '\n';
}
```

