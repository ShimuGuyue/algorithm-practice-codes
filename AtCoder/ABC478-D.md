

```cpp
void solve()
{
    int n, q;
    cin >> n >> q;

    map<int, vector<pair<int, int>>> m;
    while (q--)
    {
        int l, r, x;
        cin >> l >> r >> x;
        m[x].push_back({l, r});
    }
    for (auto& [k, v] : m)
    {
        sort(v.begin(), v.end());
    }

    vector<int> difs(n + 2);
    for (auto& [k, v] : m)
    {
        auto [l, r] = v[0];
        for (int i = 1; i < v.size(); ++i)
        {
            auto [ll, rr] = v[i];
            if (ll <= r + 1)
            {
                r = std::max(r, rr);
            }
            else
            {
                ++difs[l];
                --difs[r + 1];
                l = ll;
                r = rr;
            }
        }
        ++difs[l];
        --difs[r + 1];
    }

    vector<int64_t> as(n + 2);
    partial_sum(difs.begin(), difs.end(), as.begin());

    for (int i = 1; i <= n; ++i)
    {
        cout << as[i] << ' ';
    }
    cout << '\n';
}
```

