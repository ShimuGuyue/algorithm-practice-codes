

```c++
void solve()
{
    int n, t;
    std::cin >> n >> t;
    std::vector<int> as(n);
    for (auto& a : as)
    {
        std::cin >> a;
    }

    if (n == 0)
    {
        std::cout << t << '\n';
        return;
    }

    as.push_back(t);

    int flag{ 0 };
    int ans{ 0 };
    for (int i = 0; i <= n; ++i)
    {
        if (as[i] > flag)
        {
            ans += as[i] - flag;
            flag = as[i] + 100;
        }
    }
    std::cout << ans << '\n';
}
```

