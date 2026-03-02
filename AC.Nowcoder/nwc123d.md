

```c++
static constexpr int mod{ 998244353 };

void solve()
{
    int n;
    std::cin >> n;
    std::map<int, int> counts;
    for (int i = 0; i < n; ++i)
    {
        int a;
        std::cin >> a;
        ++counts[a];
    }

    int count2to3{ 0 };
    int count4toinf{ 0 };
    for (auto [k, v] : counts)
    {
        if (v >= 4)
            ++count4toinf;
        else if (v >= 2)
            ++count2to3;
    }

    int64_t ans{ 0 };
    for (auto [x, y] : counts)
    {
        if (!counts.count(x + 1))
            continue;
        if (y < 3 || counts[x + 1] < 3)
            continue;
        int cur2{ count2to3 };
        int cur4{ count4toinf };
        for (int count : {y, counts[x + 1]})
        {
            if (count >= 4)
                --cur4;
            else if (count >= 2)
                --cur2;
        }
        for (int count : {y - 3, counts[x + 1] - 3})
        {
            if (count >= 4)
                ++cur4;
            else if (count >= 2)
                ++cur2;
        }
        ans += cur2 * (cur2 - 1) / 2;
        ans %= mod;
        ans += cur4 * (cur4 - 1) / 2;
        ans %= mod;
        ans += cur2 * cur4;
        ans %= mod;
        ans += cur4;
        ans %= mod;
    }
    std::cout << ans << '\n';
}
```

