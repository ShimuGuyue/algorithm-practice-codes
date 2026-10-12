

```cpp
void solve()
{
    int n, m;
    cin >> n >> m;

    vector<array<int64_t, 3>> as(n * m);
    for (int i = 0; i < n; ++i)
    {
        for (int j = 0; j < m; ++j)
        {
            int a;
            cin >> a;
            as[i * m + j] = {a, i, j};
        }
    }

    sort(as.begin(), as.end(),
        [](array<int64_t, 3>& a, array<int64_t, 3>& b)
        {
            return a[0] < b[0];
        }
    );

    int64_t ans = 0;
    int l = 0, r = 0;
    while (r <= n * m)
    {
        if (r == n * m || as[l][0] != as[r][0])
        {
            sort(as.begin() + l, as.begin() + r,
                [](array<int64_t, 3>& a, array<int64_t, 3>& b)
                {
                    return a[1] < b[1];
                }
            );
            int64_t count = 0;
            int64_t sum = 0;
            int64_t last = 0;
            for (int i = l; i < r; ++i)
            {
                if (count)
                {
                    int64_t cur = last + count * (as[i][1] - as[i - 1][1]);
                    sum += cur;
                    last = cur;
                }
                ++count;
            }
            ans += sum;

            sort(as.begin() + l, as.begin() + r,
                [](array<int64_t, 3>& a, array<int64_t, 3>& b)
                {
                    return a[2] < b[2];
                }
            );
            count = 0;
            sum = 0;
            last = 0;
            for (int i = l; i < r; ++i)
            {
                if (count)
                {
                    int64_t cur = last + count * (as[i][2] - as[i - 1][2]);
                    sum += cur;
                    last = cur;
                }
                ++count;
            }
            ans += sum;

            l = r;
        }
        ++r;
    }

    ans *= 2;
    cout << ans << '\n';
}
```

