

```cpp
struct DisjointSet
{
    vector<int> fathers;

    DisjointSet(int n) : fathers(n)
    {
        iota(fathers.begin(), fathers.end(), 0);
    }

    int find(int x)
    {
        return fathers[x] == x ? x : fathers[x] = find(fathers[x]);
    }

    void merge(int x, int y)
    {
        fathers[find(x)] = find(y);
    }
};
```

```cpp
void solve()
{
    int n;
    cin >> n;
    vector<pair<int, int>> indexs(n + 1, {-1, -1});
    for (int i = 0; i < n * 2; ++i)
    {
        int a;
        cin >> a;
        if (indexs[a].first == -1)
            indexs[a].first = i;
        else
            indexs[a].second = i;
    }

    DisjointSet ds(n * 2);
    for (int i = 1; i <= n; ++i)
    {
        auto [l, r] = indexs[i];
        ds.merge(l, r);
    }

    string ans(n * 2, '\0');

    for (int i = 0; i < n * 2; i += 2)
    {
        ans[i]     = '(';
        ans[i + 1] = ')';
        ds.merge(i, i + 1);
    }

    for (int i = 1; i < n * 2; ++i)
    {
        if (ds.find(i - 1) != ds.find(i))
        {
            ds.merge(i - 1, i);
            swap(ans[i - 1], ans[i]);
        }
    }

    cout << ans << '\n';
}
```

