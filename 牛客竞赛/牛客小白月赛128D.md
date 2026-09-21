

```c++
void solve()
{
    int n, m;
    std::cin >> n >> m;
    std::vector<int64_t> as(n);
    for (int i = 0; i < n; ++i)
    {
        std::cin >> as[i];
    }

    std::vector<int64_t> bs{ as };
    std::sort(bs.begin(), bs.end());
    std::vector<int64_t> presums(n);
    std::partial_sum(bs.begin(), bs.end(), presums.begin());

    for (int i = 0; i < n; ++i)
    {
        int64_t a{ as[i] };
        int64_t b{ m - a };
        int index = std::upper_bound(bs.begin(), bs.end(), b) - bs.begin();
        int64_t ans{ 0 };
        if (b < a)
        {
            ans += a * index;
            ans -= (index == 0 ? presums[n - 1] : presums[n - 1] - presums[index - 1]) - a;
        }
        else
        {
            ans += a * (index - 1);
            ans -= (index == 0 ? presums[n - 1] : presums[n - 1] - presums[index - 1]);
        }
        std::cout << ans << ' ';
    }
    std::cout << '\n';
}
```

