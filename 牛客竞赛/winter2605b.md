

```c++
void solve()
{
    int n, m;
    std::cin >> n >> m;
    for (int i{ 1 }; i <= n; ++i)
    {
        for (int j{ 1 }; j <= m; ++j)
        {
            if ((i + j) & 1)
                std::cout << '\\';
            else
                std::cout << '/';
        }
        std::cout << '\n';
    }
}
```

