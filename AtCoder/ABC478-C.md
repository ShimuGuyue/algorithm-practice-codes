

```cpp
struct SegTree
{
    int n;
    vector<int> maxs, mins;

    SegTree(const vector<int> &as, int nn)
    {
        n = nn;
        maxs.resize(4 * n);
        mins.resize(4 * n);
        build(1, 1, n, as);
    }

    void build(int index, int l, int r, const vector<int> &a)
    {
        if (l == r)
        {
            maxs[index] = mins[index] = a[l];
            return;
        }
        int mid = (l + r) / 2;
        build(index * 2, l, mid, a);
        build(index * 2 + 1, mid + 1, r, a);
        maxs[index] = std::max(maxs[index * 2], maxs[index * 2 + 1]);
        mins[index] = std::min(mins[index * 2], mins[index * 2 + 1]);
    }

    pair<int, int> query(int index, int l, int r, int ll, int rr)
    {
        if (ll <= l && r <= rr)
            return {maxs[index], mins[index]};
        int mid = (l + r) / 2;
        if (rr <= mid)
            return query(index * 2, l, mid, ll, rr);
        if (ll > mid)
            return query(index * 2 + 1, mid + 1, r, ll, rr);
        auto left = query(index * 2, l, mid, ll, rr);
        auto right = query(index * 2 + 1, mid + 1, r, ll, rr);
        return {std::max(left.first, right.first), std::min(left.second, right.second)};
    }

    pair<int, int> query(int l, int r)
    {
        return query(1, 1, n, l, r);
    }
};
```

```cpp
void solve()
{
    int n, k;
    cin >> n >> k;
    vector<int> as(n + 2);
    for (int i = 1; i <= n; ++i)
    {
        cin >> as[i];
    }
    as[n + 1] = 1 << 30;

    int l = 1, r = n;
    vector<bool> pres(n + 2);
    vector<bool> sufs(n + 2);
    pres[0] = true;
    sufs[n + 1] = true;
    for (int i = 1; i <= n; ++i)
    {
        l = i;
        if (as[i] < as[i - 1])
            break;
        pres[i] = true;
    }

    for (int i = n; i >= 1; --i)
    {
        r = i;
        if (as[i] > as[i + 1])
            break;
        sufs[i] = true;
    }

    if (r - l + 1 > k)
    {
        cout << "No\n";
        return;
    }

    SegTree tree(as, n);

    for (int i = 1; i + k <= n + 1; ++i)
    {
        if (!pres[i - 1] || !sufs[i + k])
            continue;
        auto [max, min] = tree.query(i, i + k - 1);
        if (max > as[i + k])
            continue;
        if (min < as[i - 1])
            continue;
        cout << "Yes\n";
        return;
    }
    cout << "No\n";
}
```

