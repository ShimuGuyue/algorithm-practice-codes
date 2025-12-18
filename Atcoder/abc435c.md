

```c++
void solve()
{
    int n;
    std::cin >> n;
    std::vector<int> as(n + 1);
    for (int i = 1; i <= n; ++i)
    {
        std::cin >> as[i];
    }
    int flag{ 1 };
    for (int i = 1; i <= n; ++i)
    {
        if (i > flag)
            break;
        flag = std::max(flag, i + as[i] - 1);
    }
    int ans{ std::min(flag, n) };
    std::cout << ans << '\n';
}
```

