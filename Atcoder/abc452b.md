

```cpp
void solve()
{
    int n, m;
    std::cin >> n >> m;
    for (int i{ 1 }; i <= n; ++i)
    {
        for (int j{ 1 };j <= m; ++j)
        {
            if (i == 1 || i == n || j == 1 || j == m)
                std::cout << '#';
            else
                std::cout << '.';
        }
        std::cout << '\n';
    }
}
```

