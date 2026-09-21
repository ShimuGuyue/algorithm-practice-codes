

```c++
void solve()
{
    constexpr int64_t mod{ 1000000007 };

    int n;
    std::cin >> n;
    std::map<int64_t, int64_t> m;
    for (int i{ 0 }; i < n; ++i)
    {
        int c, w;
        std::cin >> c >> w;
        m[w] += c;
    }

    int64_t ans{ 0 };
    while (1)
    {
        if (m.size() == 1 && m.begin()->second == 1)
            break;
        auto& [k, v]{ *m.begin() };
        if (v != 1)
        {
            ans = (ans + v / 2 * 2 * k) % mod;
            m[k * 2] += v / 2;
            v = (v & 1) ? 1 : 0;
            if (v == 0)
                m.erase(k);
        }
        else
        {
            auto &[kk, vv]{ *std::next(m.begin()) };
            ans = (ans + kk + k) % mod;
            --vv;
            ++m[k + kk];
            if (vv == 0)
                m.erase(kk);
            m.erase(k);
        }
    }
    std::cout << ans << '\n';
}
```

