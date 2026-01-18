

```c++
static constexpr int64_t mod{ 998244353 };

void solve()
{
    int n;
    std::cin >> n;
    std::map<int, int> m;
    for (int i = 0; i < n; ++i)
    {
        int a;
        std::cin >> a;
        ++m[a];
    }

    int64_t ans{ 0 };
    int64_t dp{ 1 };
    for (int i = 1; i <= n; ++i)
    {
        if (m.count(i) == 0)
            break;
        int64_t v{ m[i] };
        if (v < 2)
            break;
        dp = dp * (v * (v - 1) / 2 % mod) % mod;
        ans = (ans + dp) % mod;
        debug_(dp, ans);
    }
    std::cout << ans << '\n';
}
```

