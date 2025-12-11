

```c++
void solve()
{
    constexpr int mod{ 998244353 };

    int n;
    std::cin >> n;
    std::array<int, 26> counts{};
    std::string s;
    std::cin >> s;
    for (char c : s)
    {
        ++counts[c - 'a'];
    }

    int64_t ans{ 0 };
    for (int i = 0; i < 24; ++i)
    {
        for (int j = i + 1; j < 25; ++j)
        {
            for (int k = j + 1; k < 26; ++k)
            {
                if (counts[i] == 0 || counts[j] == 0 || counts[k] == 0)
                    continue;
                int64_t cur{ 6 };
                cur *= counts[i];
                cur %= mod;
                cur *= counts[j];
                cur %= mod;
                cur *= counts[k];
                cur %= mod;
                ans += cur;
                ans %= mod;
            }
        }
    }
    std::cout << ans << '\n';
}
```

