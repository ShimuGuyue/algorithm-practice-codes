

```c++
void solve()
{
    int n, k;
    std::cin >> n >> k;

    // 维护白色区间
    std::set<std::pair<int, int>> t;
    t.insert({1, n});
    int ans{ n };
    while (k--)
    {
        int l, r;
        std::cin >> l >> r;
        auto it = t.lower_bound({l, r});
        if (it != t.begin())
            --it;
        std::vector<std::pair<int, int>> flags;
        while (it != t.end())
        {
            if (it->first > r)
                break;
            auto [ll, rr]{ *it };
            if (!(l > rr) && !(r < ll))
                flags.push_back({ll, rr});
            ++it;
        }
        for (auto [ll, rr] : flags)
        {
            if (l <= ll && r >= rr)
            {
                ans -= rr - ll + 1;
                t.erase({ll, rr});
            }
            else if (l >= ll && r <= rr)
            {
                ans -= r - l + 1;
                t.erase({ll, rr});
                t.insert({ll, l - 1});
                t.insert({r + 1, rr});
            }
            else if (l <= ll && r <= rr)
            {
                ans -= r - ll + 1;
                t.erase({ll, rr});
                t.insert({r + 1, rr});
            }
            else if (l >= ll && r >= rr)
            {
                ans -= rr - l + 1;
                t.erase({ll, rr});
                t.insert({ll, l - 1});
            }
        }
        std::cout << ans << '\n';
    }
}
```

