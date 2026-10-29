

```cpp
void solve()
{
    int n, k;
    cin >> n >> k;
    vector<int> as(n + 1);
    for (int i = 1; i <= n; ++i)
    {
        cin >> as[i];
    }

    vector<int> counts(k + 1);
    for (int i = 1; i <= n; ++i)
    {
        if (as[i] > k)
            continue;
        int flag = ((as[i] - i + 1) % k + k) % k;
        ++counts[flag];
    }

    int ans = n - *max_element(counts.begin(), counts.end());
    cout << ans << '\n';
}
```

