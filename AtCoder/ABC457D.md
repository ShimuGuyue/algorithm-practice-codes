

```cpp
void solve()
{
    int64_t n, k;
    std::cin >> n >> k;
    std::vector<int64_t> as(n + 1);
    for (int i{ 1 }; i <= n; ++i)
    {
        std::cin >> as[i];
    }

    auto check = [&as, n, k](int64_t m) -> bool
    {
        static auto ceil_div = [](int64_t a, int64_t b) -> int64_t
        {
            return (a + b - 1) / b;
        };
        int64_t sum{ 0 };
        for (int i{ 1 }; i <= n; ++i)
        {
            if (as[i] >= m)
                continue;
            int64_t dif{ m - as[i] };
            sum += ceil_div(dif, i);
            if (sum > k)
                return false;
        }
        return true;
    };

    int64_t l{ 0 }, r{ 9000000000000000000 };
    while (l < r)
    {
        int64_t mid{ (l + r + 1) / 2 };
        if (check(mid))
            l = mid;
        else
            r = mid - 1;
    }
    std::cout << l << '\n';
}
```

