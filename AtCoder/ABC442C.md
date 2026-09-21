

```c++
void solve()
{
    int n, m;
    std::cin >> n >> m;
    std::vector<int> counts(n + 1, 1);
    while (m--)
    {
        int a, b;
        std::cin >> a >> b;
        ++counts[a];
        ++counts[b];
    }
    for (int i = 1; i <= n; ++i)
    {
        std::cout << calc(n - counts[i]) << ' ';
    }
    std::cout << '\n';
}

int64_t calc(int64_t n)
{
    if (n < 3)
        return 0;
    int64_t ans{ n * (n - 1) * (n - 2) / 6 };
    return ans;
}
```

