

```c++
void solve()
{
    int n, q;
    std::cin >> n >> q;
    std::vector<std::pair<int, int>> as(n);
    for (auto& [a, b] : as)
    {
        std::cin >> a >> b;
    }

    std::vector<int> flags(n + 2, n);
    for (auto [a, b] : as)
    {
        if (a + 1 >= b - 1)
        {
            for (int i = a - 1; i <= b + 1; ++i)
            {
                --flags[i];
            }
        }
        else
        {
            for (int i = a - 1; i <= a + 1; ++i)
            {
                --flags[i];
            }
            for (int i = b - 1; i <= b + 1; ++i)
            {
                --flags[i];
            }
        }
    }

    while (q--)
    {
        int x;
        std::cin >> x;
        std::cout << flags[x] << ' ';
    }
    std::cout << '\n';
}
```

