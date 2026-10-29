

```cpp
void solve()
{
    int n, m, k;
    cin >> n >> m >> k;
    vector<array<int, 3>> xyzs(m);
    for (auto& [x, y, z] : xyzs)
    {
        cin >> x >> y >> z;
    }

    vector<int> as(n + 1);
    for (auto [x, y, z] : xyzs)
    {
        as[x] |= z;
        as[y] |= z;
    }

    for (auto a : as)
    {
        if (a > (int64_t{1} << (k + 1)) - 1)
        {
            cout << -1 << '\n';
            return;
        }
    }

    for (auto [x, y, z] : xyzs)
    {
        if ((as[x] & as[y]) != z)
        {
            cout << -1 << '\n';
            return;
        }
    }

    int64_t ans = accumulate(as.begin(), as.end(), int64_t{0});
    cout << ans << '\n';
}
```

