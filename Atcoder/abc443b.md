

```c++
void solve()
{
    int64_t n, k;
    std::cin >> n >> k;

    auto check = [n, k](int64_t m)
    {
        int64_t sum{ 0 };
        sum += n * (m + 1);
        sum += m * (m + 1) / 2;
        return sum >= k;
    };

    int l{ 0 }, r{ 100000000 };
    while (l < r)
    {
        int mid{ (l + r) / 2 };
        if (check(mid))
            r = mid;
        else
            l = mid + 1;
    }
    std::cout << r << '\n';
}
```

