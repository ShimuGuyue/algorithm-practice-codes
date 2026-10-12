

```cpp
void solve()
{
    int n, m;
    cin >> n >> m;
    vector<int> as(n + 1);
    for (int i = 1; i <= n; ++i)
    {
        cin >> as[i];
    }

    int ans = 0;
    for (int i = 1; i <= n; ++i)
    {
        for (int j = i + 1; j <= n; ++j)
        {
            for (int k = j + 1; k <= n; ++k)
            {
                if (i + j + k > m)
                    continue;
                ans = std::max(ans, as[i] + as[j] + as[k]);
            }
        }
    }
    cout << ans << '\n';
}
```

