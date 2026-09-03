

```cpp
void solve()
{
    int n, q, b;
    std::cin >> n >> q >> b;
    std::vector<int64_t> as(n + 1);
    for (int i{ 1 }; i <= n; ++i)
    {
        std::cin >> as[i];
    }
    std::vector<int> bs(n + 1);
    bs[1] = b;
    for (int i{ 2 }; i <= n; ++i)
    {
        bs[i] = bs[i - 1] == 0 ? 1 : 0;
    }

    std::vector<int64_t> pres(n + 1);
    std::partial_sum(as.begin(), as.end(), pres.begin());

    while (q--)
    {
        int64_t p;
        std::cin >> p;
        auto it = std::lower_bound(pres.begin(), pres.end(), p);
        auto loc = static_cast<int>(std::distance(pres.begin(), it));
        std::cout << bs[loc] << ' ' << loc << ' ' << p - pres[loc - 1] << '\n';
    }
}
```

