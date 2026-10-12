

```cpp
void solve()
{
    int n;
    std::cin >> n;

    if (n > 21)
    {
        std::cout << -1 << '\n';
        return;
    }

    std::vector<std::vector<int>> grid(7, std::vector<int>(6));
    int i{ 0 }, j{ 0 };
    while (n--)
    {
        grid[i][j] = 1;
        j += 2;
        if (j >= 6)
        {
            ++i;
            if (i & 1)
                j = 1;
            else
                j = 0;
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

