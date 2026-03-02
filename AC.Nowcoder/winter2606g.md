

```c++
void solve()
{
    int n, m, l;
    std::cin >> n >> m >> l;
    std::vector<int64_t> xs(n);
    for (auto& x : xs)
    {
        std::cin >> x;
    }
    std::vector<int64_t> ys(m);
    for (auto& y : ys)
    {
        std::cin >> y;
    }

    std::vector<int64_t> locs(n);
    std::partial_sum(xs.begin(), xs.end(), locs.begin());
    locs.push_back(std::numeric_limits<int64_t>::max());

    int64_t len{ 0 };
    {
        auto lt{ std::lower_bound(locs.begin(), locs.end(), len) };
        auto rt{ std::lower_bound(locs.begin(), locs.end(), len + l) };
        if (lt != rt)
        {
            std::cout << "YES\n";
            return;
        }
    }
    for (auto y :ys)
    {
        len += y;
        auto lt{ std::lower_bound(locs.begin(), locs.end(), len) };
        auto rt{ std::lower_bound(locs.begin(), locs.end(), len + l) };
        if (*lt == len)
        {
            if (lt + 1 != rt)
            {
                std::cout << "YES\n";
                return;
            }
        }
        else
        {
            if (lt != rt)
            {
                std::cout << "YES\n";
                return;
            }
        }
    }
    std::cout << "NO\n";
}
```

