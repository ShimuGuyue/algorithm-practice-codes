

```cpp
void solve()
{
    int n, m;
    cin >> n >> m;
    vector<int> as(n);
    for (auto& a : as)
    {
        cin >> a;
    }

    vector<int> factors(m + 1);
    for (int i = 2; i <= m; ++i)
    {
        for (int j = i; j <= m; j += i)
        {
            ++factors[j];
        }
    }

    int64_t ans = 0;
    for (int i = 0; i < n; ++i)
    {
        if (i != 0 && i != n - 1)
        {
            int l = i - 1, r = i + 1;
            int gcd = 0;
            while (l >= 0 && r < n)
            {
                gcd = std::gcd(gcd, abs(as[l] - as[r]));
                --l; ++r;
                ans += gcd ? factors[gcd] : m - 1;
            }
        }

        if (i != n - 1)
        {
            int l = i, r = i + 1;
            int gcd = 0;
            while (l >= 0 && r < n)
            {
                gcd = std::gcd(gcd, abs(as[l] - as[r]));
                --l; ++r;
                ans += gcd ? factors[gcd] : m - 1;
            }
        }
    }
    cout << ans << '\n';
}
```

