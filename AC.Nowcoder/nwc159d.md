

```cpp
void solve()
{
    int n, m;
    std::cin >> n >> m;
    std::vector<bool> flags(1 << m, false);
    for (int i{ 0 }; i < n; ++i)
    {
        int flag{ 0 };
        std::string s;
        std::cin >> s;
        for (int b{ 0 }; b < m; ++b)
        {
            if (s[b] == '1')
                flag |= 1 << b;
        }
        flags[flag] = true;
    }

    std::vector<int> ans(m);
    for (int b{ 0 }; b < m; ++b)
    {
        for (int i{ 0 }; i < (1 << m); ++i)
        {
            if (i >> b & 1)
                continue;
            if (flags[i] && flags[i | (1 << b)])
                ++ans[b];
        }
    }

    std::cout << std::accumulate(ans.begin(), ans.end(), 0) << '\n';
    for (auto a : ans)
    {
        std::cout << a << ' ';
    }
    std::cout << '\n';
}
```

